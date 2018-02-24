FROM centos:latest

RUN yum -y update

RUN yum -y install \
         bzip2 \
         bzip2-devel \
         gcc \
         libcurl-devel \
         libzip-devel \
         make \
         ncurses-devel \
         wget \
         xz-devel \
         zlib-devel


ENV SAMTOOLS_SOURCE="samtools-1.7.tar.bz2" \
    SAMTOOLS_VERSION="1.7" \
    SAMTOOLS_BIN="samtools" \
    SAMTOOLS_DEST="/usr/local/bin/samtools"

RUN wget https://github.com/samtools/samtools/releases/download/$SAMTOOLS_VERSION/$SAMTOOLS_SOURCE -O /opt/$SAMTOOLS_SOURCE \
    && tar -xvf /opt/$SAMTOOLS_SOURCE -C /opt \
    && cd /opt/samtools-$SAMTOOLS_VERSION \
    && ./configure \
    && make \
    && ln -s /opt/samtools-$SAMTOOLS_VERSION/$SAMTOOLS_BIN $SAMTOOLS_DEST \
    && rm /opt/$SAMTOOLS_SOURCE
