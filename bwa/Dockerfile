FROM centos:latest

RUN yum -y update

RUN yum -y install \
	bzip2 \
	gcc \
	make \
	wget \
	zlib-devel 

ENV BWA_SOURCE="bwa-0.7.15.tar.bz2" \
    BWA_VERSION="0.7.15" \
    BWA_BIN="bwa" \
    BWA_DEST="/usr/local/bin/bwa"

RUN wget https://github.com/lh3/bwa/releases/download/v$BWA_VERSION/$BWA_SOURCE -O /opt/$BWA_SOURCE \
    && tar -xvf /opt/$BWA_SOURCE -C /opt \
    && cd /opt/bwa-$BWA_VERSION \
    && make \
    && ln -s /opt/bwa-$BWA_VERSION/$BWA_BIN $BWA_DEST \
    && rm /opt/$BWA_SOURCE
