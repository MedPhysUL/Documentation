# HOWTO - Docker

## Introduction

Docker is an open-source platform that allows you to automate the deployment, scaling, and management of applications using containerization. In this guide, we will walk you through the basic steps of using Docker to run and manage containerized applications.

## Prerequisites

Before getting started, make sure you have the following:

- Docker installed on your machine. You can download it from the official Docker website (https://www.docker.com/get-started).
- Basic knowledge of the command line interface (CLI).
- Docker Desktop application running simultaneously (Windows users only).

## 1. Running your first container

1. Open your terminal or command prompt.

2. Run the following command to verify that Docker is installed and working correctly:

   ```bash
   docker --version
   ```

   This command will display the Docker version information.

3. Now, let's run a simple container to test Docker. Run the following command:

   ```bash
   docker run hello-world
   ```

   Docker will download the `hello-world` image from the Docker Hub repository (if it doesn't exist locally) and run a container based on that image.

## 2. Building and running your own image

1. Create a new directory for your project and navigate into it:

   ```bash
   mkdir myproject
   cd myproject
   ```

2. Create a file named `Dockerfile` (without any file extension) in the project directory, and open it in a text editor.

3. In the `Dockerfile`, define the instructions to build your Docker image. 

   ```
   ARG CUDA_VERSION=11.7.0
   ARG UBUNTU_VERSION=22.04
   ARG CUDNN_VERSION=8
   
   FROM nvidia/cuda:$CUDA_VERSION-cudnn$CUDNN_VERSION-devel-ubuntu$UBUNTU_VERSION
   
   # To avoid tzdata errors
   ARG DEBIAN_FRONTEND=noninteractive
   
   # Install dependencies
   RUN apt-get -y clean && \
       apt-get -y update && \
       ln -fs /usr/share/zoneinfo/America/Toronto /etc/localtime && \
       apt-get -y --no-install-recommends install build-essential wget libssl-dev libbz2-dev libreadline-dev libsqlite3-dev libffi-dev zlib1g-dev libncurses5-dev libncursesw5-dev python3-opencv  && \
       dpkg-reconfigure --frontend noninteractive tzdata
   
   # Download Python 3.11.2 source code and extract it
   RUN wget https://www.python.org/ftp/python/3.11.2/Python-3.11.2.tgz && \
       tar -xvf Python-3.11.2.tgz && \
       cd Python-3.11.2 && \
       ./configure --enable-optimizations && \
       make -j$(nproc) && \
       make install && \
       cd .. && \
       rm Python-3.11.2.tgz
   
   # Install pip
   RUN wget https://bootstrap.pypa.io/get-pip.py && \
       python3.11 get-pip.py
   
   RUN python3.11 --version
   
   RUN pip3.11 --version
   
   RUN mkdir /workspace
   
   RUN mkdir /workspace/src
   
   COPY src /workspace/src
   
   COPY requirements.txt /workspace
   
   RUN pip3 install -r /workspace/requirements.txt --extra-index-url https://download.pytorch.org/whl/cu117
   
   RUN python3.11 -c "import torch; print(torch.__version__); print(torch.cuda.is_available())"
   
   COPY main.py /workspace
   
   # Create launcher
   RUN echo "#!/bin/bash" >> /workspace/runner.sh
   RUN echo "cd /workspace" >> /workspace/runner.sh
   RUN echo "python3.11 \${1}" >> /workspace/runner.sh
   RUN chmod a+x /workspace/runner.sh
   
   ENTRYPOINT ["/workspace/runner.sh"]
   
   ```

4. Save the `Dockerfile` and return to your terminal.

5. Build the Docker image using the `docker build` command:

   ```bash
   docker build . -t myproject
   ```
   
   This command will build an image based on the instructions in the `Dockerfile` and tag it with the name `myproject`.
   
6. Once the build is complete, you can run a container using your newly created image:

   ```bash
   docker run -d --name=image1 --memory="100g" --gpus='"device=0,1"' --cpus=40 -v experiments/:/workspace/experiments:rw myproject main.py
   ```
   

## Conclusion

Congratulations! You have learned the basics of using Docker to run and manage containerized applications. This guide covered running a container, building your own image using a Dockerfile, and running a container based on your custom image. Docker has many more features and capabilities, so feel free to explore the official Docker documentation (https://docs.docker.com/) to learn more about advanced usage and container orchestration.
