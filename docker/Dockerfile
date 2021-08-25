FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04

ENV DEBIAN_FRONTEND noninteractive
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

###################################### user #####################################

ENV SHELL=/bin/bash \
    USER=evanlin \
    UID=1000 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8

ENV HOME=/home/${USER}

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid ${UID} \
    ${USER} 

RUN echo "root:root" | chpasswd
RUN echo "${USER}:111111" | chpasswd

###################################### basic tools #####################################

RUN apt-get -o Acquire::ForceIPv4=true update && apt-get -yq dist-upgrade \
    && apt-get -o Acquire::ForceIPv4=true install -yq --no-install-recommends \
    locales \
    cmake \
    make \
    git \
    vim \
    gedit \
    wget \
    nano \
    sudo \
    lsb-release \
    build-essential \
    net-tools \
    dirmngr \
    gnupg2 \
    mercurial \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    libpcap-dev \
    python-gtk2 \
    python-gobject \
    python-tk \
    python-scipy \
    python-pip \
    python3-pip \
    python3-setuptools \
    python3-opencv \
    python3-numpy \
    python3-empy  \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

##################################### PIP2 ######################################

RUN pip2 install --upgrade pip setuptools

RUN pip2 install \
    modern_robotics \
    scipy==1.2.3 

##################################### PIP3 ######################################

RUN pip3 install --upgrade pip setuptools

RUN pip3 install \
    cython \
    catkin-tools \
    matplotlib \
    pandas \
    requests \
    scikit-image \
    scikit-learn \
    gdown  \
    seaborn \
    modern_robotics \ 
    chumpy \ 
    trimesh \
    pycpd \
    easydict  \
    shapely \
    lmdb \ 
    colour \ 
    pyrr \
    plotly \
    progress \
    rtree \
    sk-video \
    yacs \
    tqdm \
    jupyter

RUN pip3 install \
    torch==1.6.0+cu101 \
    torchvision==0.7.0+cu101 \
    -f https://download.pytorch.org/whl/torch_stable.html

RUN pip3 install \
    torchaudio -f https://download.pytorch.org/whl/torch_stable.html

##################################### setting #####################################
RUN chown -R ${USER}:${USER} ${HOME}/
RUN echo "arg-medical ALL=(ALL)  ALL" > /etc/sudoers

# Support of nvidia-docker 2.0
ENV NVIDIA_VISIBLE_DEVICES=all
ENV NVIDIA_DRIVER_CAPABILITIES=all

# setup entrypoint
USER ${USER}

WORKDIR ${HOME}
