FROM ubuntu:18.04

ARG uid=1000
ARG user=indy

RUN apt-get update -y && apt-get install -y \
        apt-transport-https \
        ca-certificates \
        git \
        wget \
        unzip \
        python3-pip \
        python3-dev \
        python3-venv \
        libsodium23 \
        iptables \
        at \
        supervisor \
        libsnappy-dev \
        zlib1g-dev \
        libbz2-dev \
        liblz4-dev \
        libzstd-dev \
        libgflags-dev \
        build-essential \
        librocksdb5.8 \
        librocksdb-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install -U \ 
	'pip<10.0.0' \
	setuptools==50.3.2 \
	pep8==1.7.1 \
	pep8-naming==0.6.1 \
	flake8==3.5.0 
# fails when executed in one command with other pip install packages
RUN pip install python-rocksdb

# Indy Node and Plenum
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys CE7709D068DB5E88 && \
    echo "deb https://repo.sovrin.org/deb bionic master" >> /etc/apt/sources.list && \
    apt-get update && apt-get install -y \ 
    ursa=0.3.2-1
    
# Indy SDK
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys CE7709D068DB5E88 || \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CE7709D068DB5E88 && \
    echo "deb https://repo.sovrin.org/sdk/deb bionic master" >> /etc/apt/sources.list && \
    apt-get update -y && apt-get install -y \ 
    libindy=1.13.0~1420

USER $user
WORKDIR /home/$user

