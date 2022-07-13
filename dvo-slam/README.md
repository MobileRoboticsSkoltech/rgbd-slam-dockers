# DVO-SLAM Docker image
This repo contains ready Dockerfile for building DVO-SLAM image.

## Building and using Docker image

At first you need to build Docker image.
```
cd PATH_TO_REPOSITORY/dvo-slam/DVO-SLAM
docker build -t dvo-slam:latest .
```

Then you can follow the [original instructions](https://github.com/vnmsklnk/docker_dvo_slam/tree/e4a5b50fa28cb7cc678736babe4d746b44cdf7d2#usage) for running and using the Docker image.

## Editing startup parameters

Our modification of DVO-SLAM supports modification of intrinsic camera parameters by editing `docker_dvo_slam/dvo_benchmark/launch/benchmark.launch`.