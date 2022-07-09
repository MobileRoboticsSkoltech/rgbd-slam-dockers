FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

ENV PROJECT_DIR="/BundleFusion/"

RUN apt-get update \
	&& apt-get --no-install-recommends install -y \
	build-essential \
	cmake \
	git \
	gnupg \
	libeigen3-dev \
	libfreeimage-dev \
	libncurses-dev \
	libopencv-dev \
	software-properties-common \
	wget 

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb \    
	&& dpkg -i cuda-keyring_1.0-1_all.deb \
	&& add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /" \
	&& apt-get update \
	&& apt-get --no-install-recommends install -y cuda-11-4

COPY BundleFusionUbuntu $PROJECT_DIR

RUN cd $PROJECT_DIR \
	&& mkdir build \
	&& cd build \
	&& cmake .. \
	&& make -j8
