# DROID-SLAM Docker image
This repo contains ready Dockerfile for building DROID-SLAM image. It supports original DROID-SLAM version as well as our modification with RGB-D cameras support.

## Building and launching Docker image

At first you need to build Docker image.
```
cd PATH_TO_REPOSITORY/droid-slam
docker build droid-slam:latest .
```

Then you can run Docker image with this command:
```
docker run -it --rm --net=host -e DISPLAY=$DISPLAY \
           -v PATH_TO_YOUR_LOCAL_DATA:/dataset droid-slam:latest
```

## Using Docker image

You can follow the [original instructions](https://github.com/KonstantinPakulev/DROID-SLAM#demos) for running and using the Docker image.

*NOTE:* `droid.pth` file is already available in the image.

Also you can use DROID-SLAM in RGB-D mode. Example of startup script you can see [here](https://github.com/KonstantinPakulev/DROID-SLAM/blob/main/tools/evaluate_sam_office.sh).

## Editing startup parameters

You can edit path to dataset (`SAM_PATH`), path to associations file (`ASSOC_PATH`), path to output file with trajectory (`OUTPUT_FILE`) and path to weights (`WEIGHTS_PATH`) in [startup script](https://github.com/KonstantinPakulev/DROID-SLAM/blob/main/tools/evaluate_sam_office.sh). 

*NOTE:* you should have `color` and `depth` folders in `SAM_PATH`.

Intrinsic camera parameters can be modified in `SAM_PATH/camera_params.npy`.