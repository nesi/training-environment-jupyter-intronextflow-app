FROM ubuntu:22.04

# run unminimise, e.g. for man pages to work
RUN yes | unminimize

# install system dependencies
# TODO: move ldap-utils, libnss-ldapd, libpam-ldapd, nscd, nslcd to base image??
RUN echo 'tzdata tzdata/Areas select Pacific' | debconf-set-selections \
    && echo 'tzdata tzdata/Zones/Pacific select Auckland' | debconf-set-selections \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bioawk \
        curl \
        fakeroot \
        file \
        git \
        ldap-utils \
        libnss-ldapd \
        libpam-ldapd \
        less \
        locales \
        man-db \
        nano \
        nodejs \
        nscd \
        nslcd \
        python-is-python3 \
        python3 \
        python3-pip \
        rsync \
        software-properties-common \
        tzdata \
        unzip \
        vim \
        wget \
        zip \
        openjdk-17-jdk openjdk-17-jre \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_NZ -c -f UTF-8 -A /usr/share/locale/locale.alias en_NZ.UTF-8

ENV LANG en_NZ.utf8

# install apptainer
RUN add-apt-repository -y ppa:apptainer/ppa \
    && apt update \
    && apt install -y apptainer-suid \
    && rm -rf /var/lib/apt/lists/*

#install nextflow : Download -all from GH to workaround https://github.com/nesi/training-environment-jupyter-intronextflow-app/issues/1
#RUN curl -s https://get.nextflow.io | bash \
RUN wget -c https://github.com/nextflow-io/nextflow/releases/download/v23.10.1/nextflow-23.10.1-all \
    && mv nextflow-23.10.1-all nextflow \ 
    && chmod +x nextflow \
    && mv nextflow /usr/local/bin \
    && chmod a+rw /usr/local/bin/nextflow

# install jupyterlab and nf-core
RUN pip3 --no-cache-dir install jupyterlab
RUN pip3 --no-cache-dir install nf-core
