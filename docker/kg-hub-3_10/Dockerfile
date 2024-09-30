FROM ubuntu:22.04

RUN echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/00-docker

RUN echo 'APT::Install-Recommends "0";' >> /etc/apt/apt.conf.d/00-docker

RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update \
  && apt-get install -qyy build-essential curl wget tmux byobu htop musl-tools binutils \
  && apt-get install -y curl git maven emacs nano software-properties-common \
  && apt-get install -y python3 python3.10-venv python3-pip \
  && rm -rf /var/lib/apt/lists/* \
  && useradd -u 114 -ms /bin/bash jenkinsuser \
  && su jenkinsuser \
  && pip3 install awscli boto3 kgx multi-indexer oaklib pystache s3cmd
