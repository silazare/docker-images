FROM ubuntu:bionic

RUN set -ex && \
    apt-get -qq update && \
    apt-get -qq -y install apt-transport-https \
      curl \
      gnupg2 \
      gettext-base

RUN set -ex && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | \
    tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
    apt-get update -qq && \
    apt-get -qq -y install google-cloud-sdk && \
    mkdir -p /usr/lib64/google-cloud-sdk/bin && \
    ln -s /usr/bin/gcloud /usr/lib64/google-cloud-sdk/bin/gcloud

RUN set -ex && \
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list && \
    apt-get update -qq && \
    apt-get install -y kubectl && \
    apt-get clean autoclean && \
    apt-get autoremove && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

CMD ["bash"]