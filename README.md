# racecar-mn

## Drivers


```sh
# USB Wifi Dongle
# Source: https://devtalk.nvidia.com/default/topic/1049303/jetson-nano/jetson-nano-wifi-/2
echo "blacklist rtl8192cu" | sudo tee -a /etc/modprobe.d/blacklist.conf
echo options rtl8xxxu ht40_2g=1 dma_aggregation=1 | sudo tee /etc/modprobe.d/rtl8xxxu.conf
```

## Software Setup

Note: Assumes username/hostname is `racecar@racecar`

```sh
# setup folders
mkdir -p ~/racecar_ws/.catkin_ws/src
mkdir ~/racecar_ws/jupyter_ws
mkdir ~/.jupyter

# setup .scripts folder
cd ~/racecar_ws
git clone https://github.com/fishberg/mn-scripts. .scripts

# setup home directory symlinks
ln -s ~/racecar_ws/.scripts/_vimrc ~/.vimrc
ln -s ~/racecar_ws/.scripts/_tmux.conf ~/.tmux.conf

# config jupyter
ln -s ~/racecar_ws/.scripts/jupyter_notebook_config.py ~/.jupyter/jupyter_notebook_config.py

# add racecar _bashrc to ~/.bashrc
echo "source /home/racecar/racecar_ws/.scripts/_bashrc" >> ~/.bashrc

# setup ROS workspace
cd ~/racecar_ws/.catkin_ws/src
git clone https://github.com/fishberg/racecar_mn.git
git clone https://github.com/EAIBOT/ydlidar.git

# build ROS workspace
cd ~/racecar_ws/.catkin_ws
catkin_make
```

Open the user crontab file with `crontab -e` and add the following line:
```
@reboot /home/racecar/racecar_ws/.scripts/cron_jupyter.bash
```
