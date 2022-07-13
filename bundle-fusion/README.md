# BundleFusion Docker image
This repo contains ready Dockerfile for building BundleFusion image.

## Building and launching Docker image

At first you need to build Docker image.
```
cd PATH_TO_REPOSITORY/bundle-fusion
docker build -t bundle-fusion:latest .
```

Then you can run Docker image with this command:
```
docker run -it --rm --net=host -e DISPLAY=$DISPLAY \
           -v PATH_TO_YOUR_LOCAL_DATA:/dataset \
           --gpus all bundle-fusion:latest
```

## Using Docker image

Now you can run BundleFusion:
```
cd /BundleFusion/build
./bundle_fusion_example ../zParametersDefault.txt \
../zParametersBundlingDefault.txt  /dataset
```

## Editing startup parameters

All necessary settings such as intrinsic camera parameters, shape of images and etc. can be changed in the `zParametersDefault.txt` and `zParametersBundlingDefault.txt` files.