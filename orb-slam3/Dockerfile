FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

ENV PROJECT_DIR="/ORB_SLAM3/"

RUN apt-get update \
	&& apt-get install -y \
	build-essential \ 
	cmake \
	git \
	libavcodec-dev \ 
	libavformat-dev \
	libboost-all-dev \
	libgl1-mesa-dev \
	libglew-dev \
	libgtk2.0-dev \
	libeigen3-dev \
	libssl-dev \
	libswscale-dev \
	libopencv-dev \
        pkg-config

# Build Pangolin for visualization
RUN git clone https://github.com/stevenlovegrove/Pangolin.git \
	&& cd Pangolin \
	&& mkdir build \
	&& cd build \
	&& cmake .. -D CMAKE_BUILD_TYPE=Release \
	&& make -j 4 \
	&& make install

COPY ORB_SLAM3 $PROJECT_DIR

# Dirty hack to low OpenCV requirements
RUN sed -i "s/find_package(OpenCV 4.4)/find_package(OpenCV 4.2)/g" $PROJECT_DIR/CMakeLists.txt

# Hack not to freeze build on systems with less kernels (slows down build a little) 
RUN sed -i "s/make -j4/make/g" $PROJECT_DIR/build.sh

RUN cd $PROJECT_DIR \
	&& ./build.sh \
	&& ldconfig

