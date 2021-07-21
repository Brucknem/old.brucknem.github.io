---
layout: post
title:  "How to setup mujoco-py and robosuite"
date:   2021-07-21 10:20:00 +0200
categories: Coding
tags: coding tutorials
pin: false
---

# Installation

## Install dependencies
```shell
sudo apt install libosmesa6-dev libgl1-mesa-glx libglfw3
sudo ln -s /usr/lib/x86_64-linux-gnu/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
```

### Optional: Install virtualenv 
```shell
pip3 install virtualenv
```

## Create virtualenv
```shell
# Change python3.8 to your version
virtualenv -p /usr/bin/python3.8 venv  
source venv/bin/activate
```

## Install packages
```shell
python -m pip install -I mujoco-py
python -m pip install -I robosuite
```

# Setup

## Command Line
```shell
# Bash
$SHELL_TYPE=bash
# ZSH
$SHELL_TYPE=zsh

echo "export LD_LIBRARY_PATH=\$LD_LIBRARY_PATH:/home/$USER/.mujoco/mujoco200/bin" >> ~/.$SHELL_TYPE"rc"
echo "export LD_PRELOAD=\$LD_PRELOAD:/usr/lib/x86_64-linux-gnu/libGLEW.so" >> ~/.$SHELL_TYPE"rc"

source ~/.$SHELL_TYPE"rc"
```

## PyCharm
Add the following to the `Environment variables` in the run configs.
```
;LD_LIBRARY_PATH=/home/brucknem/.mujoco/mujoco200/bin;LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so
```

### To apply it to all future created run configs:
- Open any run config
- Click on lower left: `Edit configuration templates...`
- Add the above to the `Environment variables`


# References

- [mujoco-py](https://github.com/openai/mujoco-py)
- [robosuite](https://github.com/ARISE-Initiative/robosuite)
