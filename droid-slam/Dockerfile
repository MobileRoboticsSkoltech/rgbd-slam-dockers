FROM continuumio/anaconda3:latest

ARG DEBIAN_FRONTEND=noninteractive

ENV PROJECT_DIR="/DROID_SLAM/"

COPY DROID_SLAM $PROJECT_DIR

RUN cd $PROJECT_DIR \
	&& conda env create -f environment.yaml
	
RUN apt-get update \
	&& apt-get install -y gnupg2 software-properties-common \
	&& apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/3bf863cc.pub \
	&& add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/ /" \
	&& add-apt-repository contrib \
	&& apt-get update \
	&& apt-get -y install cuda
	
ENV BASH_ENV ~/.bashrc
SHELL ["/bin/bash", "-c"]

RUN conda activate droidenv \
	&& pip install evo --upgrade --no-binary evo \
	&& pip install gdown \
	&& cd $PROJECT_DIR \
	&& python setup.py install
	
RUN echo "conda activate droidenv" >> ~/.bashrc
	
RUN wget -O $PROJECT_DIR/droid.pth "https://drive.google.com/uc?export=download&id=1PpqVt1H4maBa_GbPJp4NwxRsd9jk-elh"

