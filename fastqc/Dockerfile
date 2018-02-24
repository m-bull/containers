FROM centos:latest

RUN yum -y update

RUN yum -y install \
	java-1.8.0-openjdk \
	perl \
	unzip

ENV FASTQC_BIN="fastqc_v0.11.5.zip"

RUN curl -fsSL http://www.bioinformatics.babraham.ac.uk/projects/fastqc/$FASTQC_BIN -o /opt/$FASTQC_BIN \
    && unzip /opt/$FASTQC_BIN -d /opt/ \
    && chmod 755 /opt/FastQC/fastqc \
    && ln -s /opt/FastQC/fastqc /usr/local/bin/fastqc \
    && rm /opt/$FASTQC_BIN
