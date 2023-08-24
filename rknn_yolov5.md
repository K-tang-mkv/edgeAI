# RKNN yolov5 deploy

## Docker way
先拉取rknn的仓库，如果有请跳过
```
git clone https://github.com/rockchip-linux/rknn-toolkit2/tree/master
```
在Ubuntu上配置docker服务
```
curl https://get.docker.com | sh   && sudo systemctl --now
enable docker
```
进入到dockerfile的目录
```
cd rknn-toolkit2-master/docker/docker_file/ubuntu_18_04_cp36/
```
当前目录下dockerfile为Dockerfile_ubuntu_18_04_for_cp36，将其改名为Dockerfile，以便生成镜像
```
cp Dockerfile_ubuntu_18_04_for_cp36 Dockerfile
```
生成镜像
```
docker build -t rknn-ubuntu1804-cp36 ./
```
创建容器
```
docker run -v {path_to}/yolov5-xiaolunwen/:/yolov5-rknn --network host --shm-size 16G --privileged --name rknn-yolov5 -d rknn_ubuntu1804_cp36:latest tail -f /dev/null
```
进入容器
```
docker exec -it rknn-yolov5 bash
```
进入工作目录, 测试脚本
```
cd /yolov5-rknn/rknn-toolkit2-master/examples/onnx/yolov5
python3 test.py
```
