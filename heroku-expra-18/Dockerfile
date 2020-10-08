FROM heroku/heroku:18

ENV DEBIAN_FRONTEND noninteractive


RUN apt-get update && apt-get install -y wget build-essential apt-transport-https software-properties-common
# add Xpra GPG key
RUN wget -q https://xpra.org/gpg.asc -O- | apt-key add -
# add Xpra repository
RUN add-apt-repository "deb https://xpra.org/ bionic main"
# install Xpra package
RUN ls
RUN apt-get update
RUN apt-get install -y git make cmake
RUN apt-get install -y xpra

RUN apt-get install -y qt5-default libqt5svg5-dev x11-apps git

RUN useradd -ms /bin/bash myuser
USER myuser


RUN cd /home/myuser && git clone https://github.com/BehaviorTree/Groot.git && cd Groot && git submodule update --init
RUN cd /home/myuser/Groot && mkdir build && cd build && cmake .. && make -j4

USER root

RUN apt-get install -y dh-python/bionic iproute2/bionic-updates  libatm1/bionic libgdk-pixbuf2.0-bin/bionic  libgomp1/bionic-updates  libmnl0/bionic libpython3-dev/bionic-updates  libpython3.6-dev/bionic-updates  libpython3.6/bionic-updates  libxtables12/bionic  netpbm/bionic  openssh-server/bionic-updates  openssh-sftp-server/bionic-updates python-pip-whl/bionic-updates  python3-certifi/bionic python3-chardet/bionic python3-crypto/bionic  python3-dev/bionic-updates python3-distutils/bionic-updates python3-keyring/bionic python3-keyrings.alt/bionic  python3-lib2to3/bionic-updates python3-pip/bionic-updates python3-pkg-resources/bionic python3-requests/bionic-updates  python3-secretstorage/bionic python3-setuptools/bionic  python3-urllib3/bionic-updates python3-wheel/bionic python3.6-dev/bionic-updates ssh-import-id/bionic-updates


# RUN rmdir /run/user
# RUN cd /run && mkdir user
# RUN cd /run && ln -v -s /tmp user
RUN cd /run && ln -v -s /tmp xpra

RUN ls -l /run

#RUN cd /run/user && n=1; max=65536; while [ "$n" -le "$max" ]; do mkdir "$n"; n=`expr "$n" + 1`; done
RUN cd /run/user && n=1; max=65536; while [ "$n" -le "$max" ]; do ln -v -s /tmp "$n"; n=`expr "$n" + 1`; done

RUN cd /run/user && ls -l




USER myuser

#ENV XDG_RUNTIME_DIR /tmp
# RUN cd /home/myuser && python -m SimpleHTTPServer $PORT

#CMD cd /home/myuser && python -m SimpleHTTPServer $PORT
CMD XDG_RUNTIME_DIR=/tmp xpra start --no-daemon --bind-tcp=0.0.0.0:$PORT --speed=100 --file-transfer=yes --start=/home/myuser/Groot/build/Groot
# CMD XDG_RUNTIME_DIR=/tmp xpra start --bind-tcp=0.0.0.0:43452 --speed=100 --file-transfer=yes --start=/home/myuser/Groot/build/Groot &&  cd / && python -m SimpleHTTPServer $PORT
