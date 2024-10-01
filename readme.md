##  for server:
### Setup:
1. sudo docker run -it --privileged --runtime=nvidia -p 5556:5556 --entrypoint bash -v /dev:/dev -v ~/Desktop/bridge_data_robot/usb_connector_chart.yml:/tmp/camera_connector_chart -v ~/Desktop/bridge_data_robot/widowx_envs:/home/robonet/widowx_envs robonet-base
2. sudo pip install --upgrade scipy
3. sudo apt install tmux

### Starting Server:
1. roslaunch widowx_controller launch.launch python_node:=true realsense:=false camera_connector_chart:=/tmp/camera_connector_chart

2. widowx_env_service --server

## For Client:
```bash
git clone https://github.com/youliangtan/edgeml.git
cd edgeml
pip install -e .
cd ..

git clone https://github.com/rail-berkeley/bridge_data_robot.git
cd bridge_data_robot/widowx_envs
pip install -r requirements.txt
pip install -e .

cd /widowx_envs
python widowx_env_service.py --client
```


#### old in case useful
```
In tmux:
# 1. roslaunch widowx_controller widowx_rs.launch python_node:=false realsense:=false
1. roslaunch widowx_controller launch.launch python_node:=true realsense:=false camera_connector_chart:=/tmp/camera_connector_chart
#(1. with camera: exec roslaunch widowx_controller widowx_rs.launch \
    ${video_stream_provider_string} camera_connector_chart:=/tmp/camera_connector_chart \
    serial_no_camera1:=${REALSENSE_SERIAL} \
    python_node:=false realsense:=true)
#2. go_sleep

widowx_env_service --server

widowx_env_service --client

export PYTHONPATH="/usr/local/lib/python3.8/site-packages:$PYTHONPATH"
```
