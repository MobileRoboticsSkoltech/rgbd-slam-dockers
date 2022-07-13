# PlanarSLAM Docker image
This repo contains ready Dockerfile for building PlanarSLAM image.

## Building and launching Docker image

At first you need to build Docker image.
```
cd PATH_TO_REPOSITORY/planar-slam
docker build -t planar-slam:latest .
```

Then you can run Docker image with this command:
```
docker run -it --rm --net=host -e DISPLAY=$DISPLAY \
           -v PATH_TO_YOUR_LOCAL_DATA:/dataset planar-slam:latest
```

## Using Docker image

Now you can run PlanarSLAM:
```
/PlanarSLAM/Examples/RGB-D/Planar_SLAM /PlanarSLAM/Vocabulary/ORBvoc.txt \
/dataset/SETTINGS_YAML_FILE /dataset /dataset/ASSOCIATIONS_FILE
```

## Editing startup parameters

All necessary settings such as intrinsic camera parameters, shape of images and etc. can be changed in the configuration .yaml file.