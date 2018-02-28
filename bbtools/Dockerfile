FROM centos:latest

RUN yum -y update

RUN yum -y install \
	java-1.8.0-openjdk \
        wget

ENV BBTOOLS_BIN="BBMap_37.92.tar.gz" \
    BBTOOLS_DIR="bbmap" \
    BBTOOLS_DEST="/usr/local/bin"

RUN wget https://downloads.sourceforge.net/project/bbmap/$BBTOOLS_BIN -O /opt/$BBTOOLS_BIN \
    && cd /opt \
    && tar -xvzf /opt/$BBTOOLS_BIN \
    && rm /opt/$BBTOOLS_BIN

RUN for i in $(find /opt/$BBTOOLS_DIR -maxdepth 1 -type f -executable); \
    do ln -s $i $BBTOOLS_DEST; \
    done
