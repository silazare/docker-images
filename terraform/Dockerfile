FROM public.ecr.aws/amazonlinux/amazonlinux:2 as aws-cli

RUN set -ex && \
    yum update -y && \
    yum install -y unzip && \
    curl \
      --silent \
      --show-error \
      --fail \
      --remote-name "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" \
      -o "awscli-exe-linux-x86_64.zip" && \
    unzip awscli-exe-linux-x86_64.zip && \
    # The --bin-dir is specified so that we can copy the
    # entire bin directory from the installer stage into
    # into /usr/local/bin of the final stage without
    # accidentally copying over any other executables that
    # may be present in /usr/local/bin of the installer stage.
    ./aws/install --bin-dir /aws-cli-bin/

####
FROM public.ecr.aws/amazonlinux/amazonlinux:2 as terraform

ARG TERRAFORM_VERSION=1.3.7

WORKDIR /workspace

RUN set -ex && \
    yum update -y && \
    yum install -y unzip && \
    curl \
        -O \
        --silent \
        --show-error \
        --fail \
        --remote-name https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip

####
FROM public.ecr.aws/amazonlinux/amazonlinux:2

RUN set -ex && \
    yum update -y && \
    yum install -y less groff && \
    yum clean all

COPY --from=aws-cli /usr/local/aws-cli/ /usr/local/aws-cli/
COPY --from=aws-cli /aws-cli-bin/ /usr/local/bin/
COPY --from=terraform /workspace/terraform /usr/local/bin/terraform

CMD ["bash"]
