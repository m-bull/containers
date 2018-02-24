FROM mbull/bioinformatics-containers:fastqc

RUN yum -y update

RUN yum -y install \
	epel-release \
	wget

RUN yum -y install python2-pip

ENV TRIMGALORE_VERSION="0.4.5" \
    TRIMGALORE_SOURCE="TrimGalore-0.4.5" \
    CUTADAPT_VERSION="1.16"

RUN pip2 install cutadapt==$CUTADAPT_VERSION

RUN wget https://github.com/FelixKrueger/TrimGalore/archive/$TRIMGALORE_VERSION.zip -O /opt/$TRIMGALORE_VERSION.zip \
    && unzip /opt/$TRIMGALORE_VERSION -d /opt/ \
    && chmod 755 /opt/$TRIMGALORE_SOURCE/trim_galore \
    && ln -s /opt/$TRIMGALORE_SOURCE/trim_galore /usr/local/bin/trim_galore \
    && rm /opt/$TRIMGALORE_VERSION.zip
