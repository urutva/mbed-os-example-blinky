# ARG VARIANT=""
FROM mbed/mbed-os-env-cmake:latest

# This Dockerfile contains things useful for an interactive development environment
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ENV LANG en_US.utf8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Tools and config missing from the build image
RUN apt-get update
RUN apt-get install -y locales && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
RUN apt-get -fy install vim sudo bash-completion build-essential gdb docker.io
RUN pip3 install mbed-tools -U

# Create the user
RUN groupadd -g $USER_GID $USERNAME
RUN useradd -s /bin/bash -u $USER_UID -g $USER_GID -G docker -m $USERNAME
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME
RUN chmod 0440 /etc/sudoers.d/$USERNAME

# Temporarily copy gcc arm compiler to `vscode` user home directory. This should
# be fixed on the docker image `mbed/mbed-os-env-cmake`.
RUN cp -r /root/gcc-arm-none-eabi-9-2019-q4-major /home/vscode/

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************
