# Use NVIDIA's CUDA base image with Python 3.10 and CUDA 12.x
FROM nvidia/cuda:12.6.2-cudnn-runtime-ubuntu20.04

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Etc/UTC

# Install system dependencies and Python 3.10
RUN apt-get update && \
    apt-get install -y software-properties-common ffmpeg vim && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y python3.10 python3.10-dev python3.10-distutils \
    wget nano vim htop libgl1-mesa-glx libglib2.0-0 && \
    rm -rf /var/lib/apt/lists/*

# Install pip for Python 3.10
RUN wget https://bootstrap.pypa.io/get-pip.py && \
    python3.10 get-pip.py && \
    rm get-pip.py

# Set Python 3.10 and pip3 as default
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 1 && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.10 1

# Install Python dependencies
RUN python3.10 -m pip install --upgrade pip && \
    python3.10 -m pip install \
    opencv-python-headless \
    matplotlib \
    jupyter \
    ipython \
    numpy \
    boto3 \
    ultralytics && \
    rm -rf ~/.cache/pip

# Create app directory
WORKDIR /app

# Command to keep the container running
CMD ["sleep", "infinity"]
