<p align="center"><img width="40%" src="./imgs/pytorch_logo_2018.svg"></p>

---------------------------------------------------------------------

**Non-Euclidean Graph Representation 데이터**를 다루기 위한 PyTorch 튜토리얼 (PyTorch KR Tutorial Competition 2018 참가작)

## Table of Contents
- [1. Going Beyond Euclidean Data : Graphs](./1_Going_Beyond_Euclidean_Data/)
- [2. Understanding Graphs : Planetoid Dataset](./2_Understading_Graphs/)
- [3. Graph Node Classification : Spectral](./3_Spectral_Graph_Convolution/)
- [4. Graph Node Classification : Spatial](./4_Spatial_Graph_Convolution/)

## Requirements

- Install docker
For more details, see [here](https://subicura.com/2017/01/19/docker-guide-for-beginners-2.html), [here](https://hiseon.me/2018/02/19/install-docker/)
```bash
# 오래된 버전의 도커가 존재하는 경우, 오래된 버전의 도커 삭제
$ sudo apt-get remove docker docker-engine docker.io

# 도커에 필요한 패키지 설치
$ sudo apt-get update && sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

# 도커의 공식 GPG 키와 저장소를 추가한다.
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   xenial \
   stable"
# change `lsb_release -cs` to `xenial` (https://stackoverflow.com/questions/41133455/docker-repository-does-not-have-a-release-file-on-running-apt-get-update-on-ubun)

# 도커 패키지 검색 확인
$ sudo apt-get update && sudo apt-cache search docker-ce
# > docker-ce - Docker: the open-source application container engine

# 도커 CE 에디션 설치
$ sudo apt-get update && sudo apt-get install docker-ce

# 도커 사용자계정 추가
$ sudo usermod -aG docker $USER
```

- nvidia-docker 설치하기(GPU 환경)

```bash
# pytorch 1.0 cuda 10 version 을 실행하기 위해서는 nvidia-driver 396 이상을 설치하여야 한다.
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo apt-get install nvidia-396
```

```bash
# nvidia docker 설치
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -

$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list

$ sudo apt-get update

# nvidia-docker 설치
$ sudo apt-get install -y nvidia-docker2
```

- Building your own image : Dockerfile -> Build
베이스 이미지를 받은 상태에서, 필요한 것들을 설치할 때 그냥 설치하면 날아갑니다.
따라서, Dockerfile을 만들어서 build하여 나만의 image를 만들면, 실행 환경을 저장할 수 있습니다.

```bash
# docker build [OPTIONS] PATH | URL | -
$ docker build -t {image name} . # 현재 경로에 Dockerfile이 있으며, {image name} 이름의 Dockerfile을 빌드함.

$ nvidia-docker run -it {image name} /bin/bash
```

- Pull docker image
```bash
$ docker pull bumsoo-graph-tutorial

# docker run -t {Docker Image} {시작 명령어} : interactive mode 로 진입
$ docker run -it nvidia/cuda:9.0-devel-ubuntu16.04 /bin/bash
```

## How to RUN?

```bash
$ nvidia-docker run -it bumsoo /bin/bash

# bin/bash 실행 후
> cd [:단원]
> python [:파일명]

# 예제
> cd 2_Understanding_Graphs/
> python preprocess_planetoid.py --dataset cora --step normalize --mode pitfall
```

```bash
$ nvidia-docker run -it bumsoo python [:단원]/[:파일].py

# Example
$ nvidia-docker run -it bumsoo python preprocess_planetoid.py --dataset cora --step normalize --mode pitfall
```

## Author
Bumsoo Kim, [@meliketoy](https://github.com/meliketoy)

Korea University, DMIS(Data Mining & Information Systems) Lab
