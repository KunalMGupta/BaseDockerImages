FROM nvidia/cuda:10.2-devel-ubuntu18.04

ENV TZ=America/Tijuana
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update --fix-missing && yes|apt-get upgrade
RUN apt-get install -y emacs apt-utils
RUN apt-get install -y wget pkg-config

ARG DEBIAN_FRONTEND=noninteractive

ENV APT_INTALL="apt-get install -y --no-install-recommends"

RUN apt-get update && $APT_INTALL \
         build-essential \
         cmake \
         git \
         openssh-client \
         curl \
         vim-gtk \
         tmux \
         zip \
         unzip \
         ca-certificates \
         libjpeg-dev \
         libopenexr-dev \
         libpng-dev \
         sudo \
         screen


ENV PIP3I="python3 -m pip install  --upgrade "

RUN $APT_INTALL \
    python3 python3-pip python3-dev python3-tk python3-pil.imagetk
RUN $PIP3I --upgrade pip
RUN $PIP3I setuptools

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH
RUN mkdir ~/.conda
RUN apt-get update --fix-missing && apt-get install -y wget bzip2 ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 \
    git mercurial subversion

RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

RUN pip install jupyterlab==3 xeus-python
RUN pip install comet_ml


ENV PATH /opt/conda/bin:$PATH
EXPOSE 8888 8889 8890 8891 8892 8893 8894 8895 8896 8897 8898 8899 8900 8901 8902 8903 8904 8905 8906 8907 8908 8909 8910 8911 8912 8913 8914 8915 8916 8917
CMD [ "/bin/bash" ]
