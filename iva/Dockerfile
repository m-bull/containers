FROM centos:latest

RUN yum -y update

RUN yum -y install epel-release

ENV IVA_VERSION="1.0.9" \
    SMALT_VERSION="0.7.6" \
    KMC_VERSION="3.0.0" \
    SAMTOOLS_SOURCE="samtools-1.7.tar.bz2" \
    SAMTOOLS_VERSION="1.7" \
    SAMTOOLS_BIN="samtools" \
    SAMTOOLS_DEST="/usr/local/bin/samtools" \
    MUMMER_SOURCE="mummer-4.0.0beta2.tar.gz" \
    MUMMER_VERSION="4.0.0beta2" \
    MUMMER_DEST="/usr/local/bin" \
    TRIMMOMATIC_VERSION="0.36"


RUN yum -y install \
         python34-pip \
         bzip2-devel \
         bzip2 \
         xz-devel \
         ncurses-devel \
         wget \
         zlib-devel \
         gcc \
         gcc-c++ \
         libzip-devel \
         libcurl-devel \
         perl \
         unzip \
         java-1.8.0-openjdk \
         make

RUN wget https://github.com/samtools/samtools/releases/download/$SAMTOOLS_VERSION/$SAMTOOLS_SOURCE -O /opt/$SAMTOOLS_SOURCE \
    && tar -xvf /opt/$SAMTOOLS_SOURCE -C /opt \
    && cd /opt/samtools-$SAMTOOLS_VERSION \
    && ./configure \
    && make \
    && ln -s /opt/samtools-$SAMTOOLS_VERSION/$SAMTOOLS_BIN $SAMTOOLS_DEST \
    && rm /opt/$SAMTOOLS_SOURCE

RUN wget https://github.com/mummer4/mummer/releases/download/v$MUMMER_VERSION/$MUMMER_SOURCE -O /opt/$MUMMER_SOURCE \
    && tar -xvf /opt/$MUMMER_SOURCE -C /opt \
    && cd /opt/mummer-$MUMMER_VERSION \
    && ./configure \
    && make \
    && rm /opt/$MUMMER_SOURCE
    
RUN for i in $(find /opt/mummer-$MUMMER_VERSION/ -executable -type f); \
    do ln -s $i $MUMMER_DEST; \
    done

RUN wget "https://sourceforge.net/projects/smalt/files/smalt-$SMALT_VERSION-static.tar.gz" && \
    tar -xvzf smalt-$SMALT_VERSION-static.tar.gz && \
    cd smalt-$SMALT_VERSION && \
    ./configure && \
    make && \
    make install

RUN wget https://github.com/refresh-bio/KMC/releases/download/v$KMC_VERSION/KMC3.linux.tar.gz && \
    tar -xvzf KMC3.linux.tar.gz && \
    mv kmc* /usr/local/bin

RUN wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-$TRIMMOMATIC_VERSION.zip && \
    unzip Trimmomatic-$TRIMMOMATIC_VERSION.zip -d /usr/local/bin/ && \
    ln -s /usr/local/bin/Trimmomatic-$TRIMMOMATIC_VERSION/trimmomatic-$TRIMMOMATIC_VERSION.jar /usr/local/bin/trimmomatic.jar

RUN pip3 install iva==$IVA_VERSION
