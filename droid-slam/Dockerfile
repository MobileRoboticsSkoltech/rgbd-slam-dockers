FROM continuumio/anaconda3:latest

ARG DEBIAN_FRONTEND=noninteractive

ENV BASH_ENV ~/.bashrc
ENV PROJECT_DIR="/DROID_SLAM/"

SHELL ["/bin/bash", "-c"]
	
# Installing CUDA	
RUN apt-get update \
	&& apt-get install -y gnupg2 software-properties-common \
	&& apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/3bf863cc.pub \
	&& add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/ /" \
	&& add-apt-repository contrib \
	&& apt-get update \
	&& apt-get -y install cuda
	
COPY DROID_SLAM $PROJECT_DIR
	
RUN cd $PROJECT_DIR \
	&& conda env create -f environment.yaml \
	&& echo "conda activate droidenv" >> ~/.bashrc \
	&& conda activate droidenv \
	&& pip install evo --upgrade --no-binary evo \
	&& pip install gdown \
	&& python setup.py install \
	&& wget -O droid.pth "https://drive.google.com/uc?export=download&id=1PpqVt1H4maBa_GbPJp4NwxRsd9jk-elh" \
	&& cp droid.pth evaluation_scripts

