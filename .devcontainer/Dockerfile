FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install sudo
RUN apt -y install git curl wget unzip vim openjdk-8-jdk

RUN useradd -ms /bin/bash -g root -G sudo -u 1001 codespace \
  && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
WORKDIR /home/codespace

ENV PUB_CACHE=/home/codespace/.pub_cache
ENV PATH="/home/codespace/flutter/bin:$PATH"

USER codespace

RUN mkdir /home/codespace/.pub_cache && /home/codespace/android && cd /home/codespace/android \
  && wget https://dl.google.com/android/repository/commandlinetools-linux-8512546_latest.zip -O /home/codespace/android/commandlinetools.zip \
  && unzip commandlinetools.zip \
  && mv cmdline-tools tools \ 
  && mkdir /home/codespace/android/cmdline-tools \
  && mv tools /home/codespace/android/cmdline-tools/

ENV ANDROID_SDK_ROOT="/home/codespace/android"
ENV ANDROID_HOME="/home/codespace/android"
ENV PATH="$PATH:$ANDROID_SDK_ROOT/cmdline-tools/tools/bin"
ENV PATH="$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin"
ENV PATH="$PATH:$ANDROID_SDK_ROOT/platform-tools"

RUN echo "y" | sdkmanager 'platform-tools' 'platforms;android-30'

RUN git clone https://github.com/flutter/flutter && \
  /home/codespace/flutter/bin/flutter config --enable-web

RUN mkdir -p /workspaces/codespaces-flutter
COPY .bashrc /home/codespace/.bashrc
