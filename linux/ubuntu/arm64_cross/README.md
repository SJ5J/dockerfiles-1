## Overview

This image is used to build the dotnet/coreclr product for arm64. This is done
by mounting the cofreclr repository into the container at:
/home/dotnet-bot/coreclr.

## Building coreclr arm using the container

**Note** that $WORKSPACE in this context is the location of the coreclr repo.

>docker run -i --rm -v $WORKSPACE:/home/dotnet-bot/coreclr -e ROOTFS_DIR=/home/dotnet-bot/rootfs/arm64 jashook/coreclr-arm64-cross:latest ./coreclr/build.sh arm64 cross checked

## Image location

The latest build of this image can be pulled from dockerhub.

>docker run -it jashook/coreclr-arm64-cross:latest

The source is available on github at https://github.com/jashook/dockerfiles/tree/master/linux/ubuntu/arm64_cross

## Building

>docker build -t jashook/coreclr-arm64-cross:latest .

## Rootfs update

Building this image does not require the arm64 emulator. There is a blob storage
location containing the latest built arm64 rootfs used for coreclr. If there is
a need to update that blob it is found at: https://clrjit.blob.core.windows.net/docker/arm64.tar.gz.

If the rootfs needs to be updated follow these steps:

1. >git clone https://github.com/dotnet/coreclr
2. >sudo ./coreclr/cross/build-rootfs arm64
3. >tar -zcvf ./coreclr/cross/rootfs/arm64.tar.gz ./coreclr/cross/rootfs/arm64
4. Upload the tar file to https://clrjit.blob.core.windows.net/docker/arm64.tar.gz