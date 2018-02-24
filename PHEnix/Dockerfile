FROM centos:latest

RUN yum -y update

RUN yum -y install epel-release

RUN yum -y install \
         bzip2 \
         bzip2-devel \
         Cython \
         gcc \
         gcc-c++ \
         git \
         java-1.8.0-openjdk \
         libcurl-devel \
         libzip-devel \
         make \
         ncurses-devel \
         numpy \
         python-devel \
         python-matplotlib \ 
         python-psycopg2 \
         python2-pip \
         unzip \
         wget \
         xz-devel \
         zlib-devel 

ENV PICARD_VERSION="2.17.10" \
    PICARD_BIN="picard.jar" \
    PICARD_DEST="/usr/local/bin/picard.jar" \
    GATK_SOURCE="GenomeAnalysisTK-3.8-1-0-gf15c1c3ef.tar.bz2" \
    GATK_VERSION="3.8-1-0-gf15c1c3ef" \
    GATK_BIN="GenomeAnalysisTK.jar" \
    GATK_DEST="/usr/local/bin/GenomeAnalysisTK.jar" \
    BWA_SOURCE="bwa-0.7.15.tar.bz2" \
    BWA_VERSION="0.7.15" \
    BWA_BIN="bwa" \
    BWA_DEST="/usr/local/bin/bwa" \
    SAMTOOLS_SOURCE="samtools-1.7.tar.bz2" \
    SAMTOOLS_VERSION="1.7" \
    SAMTOOLS_BIN="samtools" \
    SAMTOOLS_DEST="/usr/local/bin/samtools" \
    BCFTOOLS_SOURCE="bcftools-1.7.tar.bz2" \
    BCFTOOLS_VERSION="1.7" \
    BCFTOOLS_BIN="bcftools" \
    BCFTOOLS_DEST="/usr/local/bin/bcftools"

RUN wget "https://github.com/broadinstitute/picard/releases/download/$PICARD_VERSION/$PICARD_BIN" -O $PICARD_DEST
ENV PICARD_JAR=/usr/local/bin/picard.jar    

RUN curl -o $GATK_SOURCE -L "https://software.broadinstitute.org/gatk/download/auth?package=GATK-archive&version=$GATK_VERSION" \
 && tar -xjf $GATK_SOURCE \
 && mv GenomeAnalysisTK-$GATK_VERSION/$GATK_BIN $GATK_DEST \
 && rm -f $GATK_SOURCE

ENV GATK_JAR=/usr/local/bin/GenomeAnalysisTK.jar

RUN wget "https://github.com/lh3/bwa/releases/download/v$BWA_VERSION/$BWA_SOURCE" -O /opt/$BWA_SOURCE \
    && tar -xvf /opt/$BWA_SOURCE -C /opt \
    && cd /opt/bwa-$BWA_VERSION \
    && make \
    && ln -s /opt/bwa-$BWA_VERSION/$BWA_BIN $BWA_DEST \
    && rm /opt/$BWA_SOURCE

RUN wget "https://github.com/samtools/samtools/releases/download/$SAMTOOLS_VERSION/$SAMTOOLS_SOURCE" -O /opt/$SAMTOOLS_SOURCE \
    && tar -xvf /opt/$SAMTOOLS_SOURCE -C /opt \
    && cd /opt/samtools-$SAMTOOLS_VERSION \
    && ./configure \
    && make \
    && ln -s /opt/samtools-$SAMTOOLS_VERSION/$SAMTOOLS_BIN $SAMTOOLS_DEST \
    && rm /opt/$SAMTOOLS_SOURCE

RUN wget "https://github.com/samtools/bcftools/releases/download/$BCFTOOLS_VERSION/$BCFTOOLS_SOURCE" -O /opt/$BCFTOOLS_SOURCE \
    && tar -xvf /opt/$BCFTOOLS_SOURCE -C /opt \
    && cd /opt/bcftools-$BCFTOOLS_VERSION \
    && ./configure \
    && make \
    && ln -s /opt/bcftools-$BCFTOOLS_VERSION/$BCFTOOLS_BIN $BCFTOOLS_DEST \
    && rm /opt/$BCFTOOLS_SOURCE


RUN wget "https://github.com/BenLangmead/bowtie2/releases/download/v2.3.4.1/bowtie2-2.3.4.1-linux-x86_64.zip" -O /usr/local/bin/bowtie2-2.3.4.1-linux-x86_64.zip \
 && cd /usr/local/bin && unzip bowtie2-2.3.4.1-linux-x86_64.zip \
 && rm /usr/local/bin/bowtie2-2.3.4.1-linux-x86_64.zip

RUN for i in $(find /usr/local/bin/bowtie2-2.3.4.1-linux-x86_64 -executable -type f); do \
    ln -s $i /usr/local/bin; \
    done

RUN git clone https://github.com/phe-bioinformatics/PHEnix.git \
    && pip2 install -e PHEnix
