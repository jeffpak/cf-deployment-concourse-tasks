FROM ubuntu:trusty

RUN \
  apt-get update && \
  apt-get -y install \
    build-essential \
    git \
    unzip \
    wget \
    software-properties-common && \
  add-apt-repository ppa:brightbox/ruby-ng -y && \
  apt-get update && \
  apt-get -y install \
    ruby2.3 \
    ruby2.3-dev && \
  apt-get remove -y --purge software-properties-common

# jq
RUN \
  wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 --output-document="/usr/bin/jq" && \
  cd /usr/bin && \
  echo "d8e36831c3c94bb58be34dd544f44a6c6cb88568 jq" | sha1sum -c - && \
  chmod +x jq

# bosh-cli
RUN \
  wget https://s3.amazonaws.com/bosh-cli-artifacts/bosh-cli-0.0.147-linux-amd64 --output-document="/usr/bin/bosh" && \
  cd /usr/bin && \
  echo "533342d7663c3e5dc731769e157608c74dd9eccb bosh" | sha1sum -c - && \
  chmod +x bosh

# cf-cli
RUN \
  cd /tmp && \
  wget -q -O cf.deb "https://cli.run.pivotal.io/stable?release=debian64&version=6.23.1&source=github-rel" && \
  echo "b25260f46bf24d1e2586c1f4d67db3fdd89f0144 cf.deb" | sha1sum -c - && \
  dpkg -i cf.deb && \
  rm cf.deb

# bbl and dependencies
RUN \
  wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v2.3.0/bbl-v2.3.0_linux_x86-64 -P /tmp && \
  mv /tmp/bbl-* /usr/local/bin/bbl && \
  cd /usr/local/bin && \
  echo "bcb162f962fa6233b1bc8b51bbf10bed2352845e bbl" | sha1sum -c - && \
  chmod +x bbl

RUN \
  wget https://releases.hashicorp.com/terraform/0.8.4/terraform_0.8.4_linux_amd64.zip -P /tmp && \
  cd /tmp && \
  echo "190b2d404cc30227f7dec429d1f643d92fce8072 terraform_0.8.4_linux_amd64.zip" | sha1sum -c - && \
  unzip /tmp/terraform_0.8.4_linux_amd64.zip -d /tmp && \
  mv /tmp/terraform /usr/local/bin/terraform && \
  cd /usr/local/bin && \
  chmod +x terraform && \
  rm -rf /tmp/*

RUN \
  wget https://s3.amazonaws.com/bosh-init-artifacts/bosh-init-0.0.99-linux-amd64 -P /tmp && \
  mv /tmp/bosh-init-0.0.99-linux-amd64 /usr/local/bin/bosh-init && \
  cd /usr/local/bin && \
  echo "00ccaf07a11bd8206407f83f1e606e16f3475bf3 bosh-init" | sha1sum -c - && \
  chmod +x bosh-init