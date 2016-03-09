# https://github.com/bigdatagenomics/adam/releases
# ADAM 0.19.0_2.10

# to build:
# docker build -t adam:0.19.0_2.10 .

# to run
# docker run --rm -ti adam:0.19.0_2.10

FROM ubuntu:14.04
MAINTAINER Zhuyi Xue <alfred532008@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get -y install \
    openjdk-7-jre \
    wget


RUN wget http://apache.mirror.gtcomm.net/spark/spark-1.5.2/spark-1.5.2-bin-hadoop2.6.tgz \
    && tar zxf spark-1.5.2-bin-hadoop2.6.tgz \
    && rm -rfv spark-1.5.2-bin-hadoop2.6.tgz

RUN wget https://repo1.maven.org/maven2/org/bdgenomics/adam/adam-distribution_2.10/0.19.0/adam-distribution_2.10-0.19.0-bin.tar.gz \
    && tar zxf adam-distribution_2.10-0.19.0-bin.tar.gz \
    && rm -rfv adam-distribution_2.10-0.19.0-bin.tar.gz

ENV ADAM_HOME="/adam-distribution_2.10-0.19.0"
ENV SPARK_HOME="/spark-1.5.2-bin-hadoop2.6"
ENV PATH=${ADAM_HOME}/bin:${SPARK_HOME}/bin:${PATH}

RUN wget https://raw.githubusercontent.com/bigdatagenomics/adam/master/adam-core/src/test/resources/small.sam -O /tmp/small.sam

# example command. The following output is known
####
# Using ADAM_MAIN=org.bdgenomics.adam.cli.ADAMMain
# Using SPARK_SUBMIT=/spark-1.5.2-bin-hadoop2.6/bin/spark-submit
# 2016-00-00 00:00:00 WARN  NativeCodeLoader:62 - Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
# 2016-00-00 00:00:00 WARN  MetricsSystem:71 - Using default name DAGScheduler for source because spark.app.id is not set.
# SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
# SLF4J: Defaulting to no-operation (NOP) logger implementation
# SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
####
# Not sure how to resolve the WARN and SLF4J problem yet
CMD ["adam-submit", "transform", "/tmp/small.sam", "/tmp/small.adam"]

