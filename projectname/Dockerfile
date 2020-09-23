FROM ubuntu:20.04

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update && apt-get upgrade -y

## To build ex LDAP
RUN apt-get update && apt-get install -y \
    curl apt-utils apt-transport-https debconf-utils gcc build-essential g++\
    && rm -rf /var/lib/apt/lists/*

## Python libraries
RUN apt-get update && apt-get install -y \
    python3-pip python3-dev python3-setuptools \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
## Install necessary locales
RUN apt-get update && apt-get install -y locales \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen

RUN pip3 install --upgrade pip

# Git
RUN apt-get update && apt-get install -y git

# LDAP
RUN apt-get update && apt-get install -y \
  libldap2-dev \
  libsasl2-dev \
  libssl-dev

# install requirements
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

RUN mkdir /app
WORKDIR /app
COPY . /app/

# -- # DEV # -- #
ENV ENV=DEV
ENV DEBUG=1