# Docker only
Please check the origin one for official


## Option 1: build by yourself
```bash
docker build -t zhangkin/voxblox_ros -f Dockerfile .
```
## Option 2: pull directly
建议内地同学直接pull 不然catkin build里有很多3dparty 可能没法clone下来

```bash
docker pull zhangkin/voxblox_ros
```

## docker run => container
Please put your bag file in the `/home/kin/bags` or replace the path in your home,
here is my folder
```bash
kin@kin-ubuntu:~/bags$ tree -L 1
.
├── cow_eth_data
│   ├── data.bag
│   ├── voxblox_cow_extras
│   └── voxblox_cow_extras.zip
```

```bash
docker run -it --net=host --gpus all --name voxblox_ros -v /home/kin/bags:/home/kin/bags zhangkin/voxblox_ros /bin/zsh 
```
## RUN
after the link folder, you can directly build and run the launch
```bash
cd ~/catkin_ws/src/voxblox && git pull origin master
cd ~/catkin_ws && catkin build voxblox_ros && source devel/setup.zsh
roslaunch voxblox_ros cow_and_lady_dataset.launch
```

Save the mesh result and save location can be mofitied from the launch :
```bash
<param name="mesh_filename" value="/home/kin/bag/$(anon cow).ply" />
```
```bash
rosservice call /voxblox_node/save_map
```
