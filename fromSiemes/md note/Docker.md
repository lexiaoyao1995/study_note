### docker

慕课网  刘果国

其实就是一个运行项目的虚拟环境

#### 核心词汇

镜像 集装箱

仓库 超级码头

容器 运行程序的地方

去仓库把镜像拿到本地，用命令把镜像运行起来

bulid 构建镜像

ship 运输镜像

run 运行镜像

#### 镜像

镜像就是一系列文件（包括操作系统，环境和运行文件）

#### 容器

就是一个进程，看做虚拟机的文件系统

#### 仓库

把镜像传到仓库，再由设备传输到目标服务器

1、官方地址：hub.docker.com   下载速度较慢

2、国内的仓库 c.163.com 

3、也可以自己搭建

#### docker安装

##### windows

win10

https://www.docker.com/products/docker#/windows

other windows

https://www.docker.com/products/docker-toolbox

#### docker命名

第一个docker镜像

docker pull [OPTIONS] NAME [:TAG]  下载镜像0

docker images 获取本地所有镜像

docker ps 查看当前运行的容器

#### 编写自己的docker

1、dockerfile

2、docker build

