FROM ubuntu
MAINTAINER alfred532008@gmail.com


RUN localedef -i en_US -f UTF-8 en_US.UTF-8

RUN apt-get update
RUN apt-get install -y curl g++ gawk m4 make patch ruby tcl

RUN useradd -m -s /bin/bash linuxbrew
RUN echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER linuxbrew
WORKDIR /home/linuxbrew
ENV PATH /home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH
ENV SHELL /bin/bash
RUN yes |ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/linuxbrew/go/install)"
RUN brew doctor || true

#############################linuxbrew setup ends##############################

RUN sudo apt-get install -y build-essential wget git
RUN set -x \
    && wget --no-check-certificate "https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-4.0.0-Linux-x86_64.sh" \
    && bash  Anaconda3-4.0.0-Linux-x86_64.sh -b \
    && rm -v Anaconda3-4.0.0-Linux-x86_64.sh

ENV PATH /home/linuxbrew/anaconda3/bin:$PATH

RUN conda install -y ipython pandas matplotlib scikit-learn

RUN git clone --recursive https://github.com/dmlc/xgboost \
    && cd xgboost && make \
    && cd python-package && python setup.py install \
    && cd && rm -rf xgboost

# needed by import matplotlib.pyplot as plt
RUN sudo apt-get install -y libglib2.0-0 libsm6 qt4-default
