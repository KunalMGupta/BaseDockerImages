FROM nvidia/cuda:10.2-devel-ubuntu18.04

ENV TZ=America/Tijuana
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update --fix-missing && yes|apt-get upgrade
RUN apt-get install -y emacs apt-utils
RUN apt-get install -y wget pkg-config

# Install dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  build-essential \
  curl \
  ca-certificates \
  dumb-init \
  htop \
  sudo \
  git \
  openssh-client \
  curl \
  libx11-6 \
  locales \
  vim-gtk \
  lsb-release \
  zip \
  unzip \
  libjpeg-dev \
  libopenexr-dev \
  libpng-dev \
  screen \
  && rm -rf /var/lib/apt/lists/*

RUN sed -i "s/# en_US.UTF-8/en_US.UTF-8/" /etc/locale.gen \
  && locale-gen
ENV LANG=en_US.UTF-8

# Create project directory
RUN mkdir /projects

# Create a non-root user
RUN adduser --disabled-password --gecos '' --shell /bin/bash coder \
  && chown -R coder:coder /projects
RUN echo "coder ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-coder

# Install fixuid
ENV ARCH=amd64
RUN curl -fsSL "https://github.com/boxboat/fixuid/releases/download/v0.4.1/fixuid-0.4.1-linux-$ARCH.tar.gz" | tar -C /usr/local/bin -xzf - && \
  chown root:root /usr/local/bin/fixuid && \
  chmod 4755 /usr/local/bin/fixuid && \
  mkdir -p /etc/fixuid && \
  printf "user: coder\ngroup: coder\n" > /etc/fixuid/config.yml

# Install code-server
WORKDIR /tmp
ENV CODE_SERVER_VERSION=3.12.0
RUN curl -fOL https://github.com/cdr/code-server/releases/download/v${CODE_SERVER_VERSION}/code-server_${CODE_SERVER_VERSION}_${ARCH}.deb
RUN dpkg -i ./code-server_${CODE_SERVER_VERSION}_${ARCH}.deb && rm ./code-server_${CODE_SERVER_VERSION}_${ARCH}.deb
COPY ./entrypoint.sh /usr/bin/entrypoint.sh

RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc
ENV PATH /opt/conda/bin:$PATH

RUN curl -sfLO https://open-vsx.org/api/ms-toolsai/jupyter/2021.8.12/file/ms-toolsai.jupyter-2021.8.12.vsix \
 && curl -sfLO https://open-vsx.org/api/ms-python/python/2021.9.1218897484/file/ms-python.python-2021.9.1218897484.vsix \
 && code-server --install-extension ./ms-toolsai.jupyter-2021.8.12.vsix || true \
 && code-server --install-extension ./ms-python.python-2021.9.1218897484.vsix || true \
 && rm ms-toolsai.jupyter-2021.8.12.vsix \
 && rm ms-python.python-2021.9.1218897484.vsix

EXPOSE 8443 8888 8889 8890 8891 8892 8893 8894 8895 8896 8897 8898 8899 8900 8901 8902 8903 8904 8905 8906 8907 8908 8909 8910 8911 8912 8913 8914 8915 8916 8917
ENTRYPOINT ["/usr/bin/entrypoint.sh", "--bind-addr", "0.0.0.0:8443","--auth","none", "--cert", "--disable-telemetry", "."]

