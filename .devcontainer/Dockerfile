FROM docker.io/nvidia/cuda:11.6.2-devel-ubuntu20.04
LABEL maintainer="Hugging Face"
LABEL repository="diffusers"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && \
    apt install -y bash \
                   build-essential \
                   git \
                   git-lfs \
                   curl \
                   ca-certificates \
                   libsndfile1-dev \
                   python3.8 \
                   python3-pip \
                   python3.8-venv && \
    rm -rf /var/lib/apt/lists

# Create non root user and setup environment.
RUN useradd -m -d /home/user -u 1000 user

# Switch to new user and workdir.
USER 1000:1000
WORKDIR /home/user

# # make sure to use venv
# RUN python3 -m venv /opt/venv
# ENV PATH="/opt/venv/bin:$PATH"

# pre-install the heavy dependencies (these can later be overridden by the deps from setup.py)
RUN python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir \
        torch \
        torchvision \
        torchaudio \
        --extra-index-url https://download.pytorch.org/whl/cu117 && \
    python3 -m pip install --no-cache-dir \
        accelerate \
        datasets \
        hf-doc-builder \
        huggingface-hub \
        librosa \
        modelcards \
        numpy \
        scipy \
        tensorboard \
        transformers \
        deepspeed

CMD ["/bin/bash"]