FROM ubuntu:bionic-20200921


MAINTAINER esromneb


# build:
#
# docker build -t esromneb/qt-wasm/1.39.11:base base


ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y wget build-essential apt-transport-https software-properties-common
# add Xpra GPG key
RUN wget -q https://xpra.org/gpg.asc -O- | apt-key add -
# add Xpra repository
RUN add-apt-repository "deb https://xpra.org/ bionic main"
# install Xpra package
RUN apt-get update
RUN apt-get install -y xpra

RUN apt-get install -y nano cmake qt5-default libqt5svg5-dev x11-apps git

#RUN cd /root && git clone https://github.com/BehaviorTree/Groot.git && cd Groot && git submodule update --init && mkdir build && cd build && cmake .. && make -j4


RUN useradd -ms /bin/bash myuser
USER myuser


RUN cd /home/myuser && git clone https://github.com/BehaviorTree/Groot.git && cd Groot && git submodule update --init
RUN cd /home/myuser/Groot && mkdir build && cd build && cmake .. && make -j4
CMD XDG_RUNTIME_DIR=/tmp xpra start --no-daemon --bind-tcp=0.0.0.0:$PORT --speed=100 --file-transfer=yes --start=/home/myuser/Groot/build/Groot
