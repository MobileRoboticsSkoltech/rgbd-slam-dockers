FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update

RUN apt-get --no-install-recommends install -y \
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

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin \
    && mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600 \
    && apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub \
    && add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /" \
    && apt update \
    && apt --no-install-recommends install -y cuda-11-4

RUN cd /home \
    && git clone https://github.com/MobileRoboticsSkoltech/BundleFusionUbuntu.git \
    && mkdir BundleFusionUbuntu/build \
    && cd BundleFusionUbuntu/build \
    && cmake .. \
    && make -j8
