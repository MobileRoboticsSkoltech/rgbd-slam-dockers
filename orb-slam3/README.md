# ORB-SLAM3 Docker image

## Building and launching Docker image

At first you need to build Docker image.
```
cd PATH_TO_REPOSITORY/orb-slam3
sudo docker build -t NAME:TAG .
```

Then you can run Docker image with this command:
```
sudo docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix  --net=host --privileged --mount src=PATH_TO_YOUR_LOCAL_DATA,target=/dataset,type=bind NAME:TAG
```

## Using Docker image

Now you can run ORB-SLAM3.
```
ORB_SLAM3/Examples/RGB-D/rgbd_tum ORB_SLAM3/Vocabulary/ORBvoc.txt dataset/PATH_TO_SETTINGS_YAML_FILE dataset dataset/PATH_TO_ASSOCIATIONS_FILE
```

## Editing startup parameters

All necessary settings such as intrinsic camera parameters, shape of images and etc. can be changed in the configuration .yaml file.