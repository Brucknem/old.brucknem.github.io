---
layout: post
title:  "How to install the latest CMake version from source"
date:   2021-07-23 09:50:00 +0200
categories: Coding
tags: coding tutorials
pin: false
---

Run the following `shell` script to install the latest CMake version.

# Installation
```shell
# Check Version
LOCATION=$(wget https://github.com/Kitware/CMake/releases/latest 2>&1 | grep Location | awk '{print $2}')
if [ "$SHELL" = "/usr/bin/zsh" ]; then
    VERSION=(${(@s:/:)LOCATION})
else
    IFS='/' read -ra VERSION <<< "$LOCATION"
fi
VERSION=$(echo ${VERSION[-1]})
VERSION=$(echo ${VERSION:1})
echo "Installing: CMake v$VERSION"

# Download
cd /tmp
CMAKE_EXTRACTED_DIR="cmake-$VERSION"
CMAKE_ARCHIVE="$CMAKE_EXTRACTED_DIR.tar.gz"
wget https://github.com/Kitware/CMake/releases/download/v$VERSION/$CMAKE_ARCHIVE
tar xfv $CMAKE_ARCHIVE

# Install
cd $CMAKE_EXTRACTED_DIR
./bootstrap
NUM_CPU_CORES=$(grep -c ^processor /proc/cpuinfo)
make -j $NUM_CPU_CORES

sudo apt install checkinstall -y
sudo checkinstall
```

# References

- [CMake](https://cmake.org/)
