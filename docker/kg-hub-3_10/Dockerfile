FROM ubuntu:22.04

ARG THIS_ENV

ENV THIS_ENV=${THIS_ENV} \
  PYTHONFAULTHANDLER=1 \
  PYTHONUNBUFFERED=1 \
  PYTHONHASHSEED=random \
  POETRY_NO_INTERACTION=1 \
  # POETRY_VIRTUALENVS_CREATE=false \
  POETRY_CACHE_DIR='/var/cache/pypoetry' \
  POETRY_HOME='/usr/local'

RUN echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/00-docker

RUN echo 'APT::Install-Recommends "0";' >> /etc/apt/apt.conf.d/00-docker

## Install dependencies for KG-Hub builds
## including setup for Jenkins builds
## and Poetry
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update \
  && apt-get install -qyy build-essential curl wget tmux byobu htop musl-tools binutils \
  && apt-get install -y curl git maven emacs nano software-properties-common \
  && apt-get install -y python3 python3.10-venv python3-pip python3-dev python3-setuptools>=61 \
  && rm -rf /var/lib/apt/lists/* \
  && useradd -u 114 -ms /bin/bash jenkinsuser \
  && su jenkinsuser \
  && pip3 install awscli boto3 kgx multi-indexer oaklib pystache s3cmd \
  && curl -sSL https://install.python-poetry.org | python3 - \
  && curl https://sdk.cloud.google.com | bash -s -- --install-dir=/root --disable-prompts \
  && echo 'export PATH=$PATH:/root/google-cloud-sdk/bin' >> /home/jenkinsuser/.bashrc