# ORB-SLAM3 Docker image
This repo contains ready Dockerfile for building ORB-SLAM3 image. It supports original ORB-SLAM3 version as well as our modification with 2 RGB-D cameras support.

## Building and launching Docker image

At first you need to build Docker image.
```
cd PATH_TO_REPOSITORY/orb-slam3
docker build -t orb3:latest .
```

Then you can run Docker image with this command:
```
docker run -it --rm --net=host -e DISPLAY=$DISPLAY \
           -v PATH_TO_YOUR_LOCAL_DATA:/dataset orb3:latest
```

## Using Docker image

Now you can run ORB-SLAM3.

For **one-view** version use:
```
/ORB_SLAM3/Examples/RGB-D/rgbd_tum /ORB_SLAM3/Vocabulary/ORBvoc.txt \
/dataset/SETTINGS_YAML_FILE /dataset /dataset/ASSOCIATIONS_FILE
```
For **two-view** version use:
```
/ORB_SLAM3/Examples/RGB-D-Two-View/rgbd_tum_tw /ORB_SLAM3/Vocabulary/ORBvoc.txt \
/dataset/SETTINGS_YAML_FILE /dataset /dataset/ASSOCIATIONS_FILE
```

## Editing startup parameters

All necessary settings such as intrinsic camera parameters, shape of images and etc. can be changed in the configuration .yaml file.