FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

ENV PROJECT_DIR="/PlanarSLAM/"

RUN apt-get update \
	&& apt-get install -y \
	build-essential \
	cmake \
	git \
	libavcodec-dev \
	libavformat-dev \
	libboost-all-dev \
	libeigen3-dev \
	libflann-dev \
	libgl1-mesa-dev \
	libglew-dev \
	libgtk2.0-dev \
	libgtkglext1-dev \
	libpcap-dev \
	libproj-dev \
	libqhull-dev \
	libssl-dev \
	libswscale-dev \
	libv4l-dev \
	libvtk6-dev \
	libvtk6-qt-dev \
	pkg-config \
	qtbase5-dev
                
# Build PCL
RUN git clone https://github.com/PointCloudLibrary/pcl.git \
	&& cd pcl \
	&& git checkout pcl-1.9.0 \
	&& mkdir release \
	&& cd release \
	&& cmake -DCMAKE_INSTALL_PREFIX=/usr/local \ 
		 -DBUILD_GPU=ON \
		 -DBUILD_apps=ON \
		 -DBUILD_examples=ON \ 
		 -DCMAKE_INSTALL_PREFIX=/usr/local \
		 -DPCL_DIR=/usr local/share/pcl .. \
	&& make -j 4 \
	&& make install        

# Build OpenCV
RUN git clone https://github.com/opencv/opencv.git \
	&& git clone https://github.com/opencv/opencv_contrib.git \
	&& cd opencv_contrib \
	&& git checkout 3.4.1 \
	&& cd .. \
	&& cd opencv \
	&& git checkout 3.4.1 \
	&& mkdir build \
	&& cd build \
	&& cmake -DCMAKE_BUILD_TYPE=Release \
		 -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
		 -DCMAKE_INSTALL_PREFIX=/usr/local .. \
	&& make -j 4 \
	&& make install

# Build Pangolin for visualization
RUN git clone https://github.com/stevenlovegrove/Pangolin.git \
	&& cd Pangolin \
	&& git checkout v0.6 \
	&& mkdir build \
	&& cd build \
	&& cmake -D CMAKE_BUILD_TYPE=Release .. \
	&& make -j 4 \
	&& make install

COPY PlanarSLAM $PROJECT_DIR

# Hack not to freeze build on systems with less kernels (slows down build a little) 
RUN sed -i "s/make -j/make/g" $PROJECT_DIR/build.sh

# Hack for successful build on Ubuntu 20.04
RUN sed -i "s/const KeyFrame\*/KeyFrame *const/g" $PROJECT_DIR/include/LoopClosing.h

RUN cd $PROJECT_DIR \
	&& ./build.sh
