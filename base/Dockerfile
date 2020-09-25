FROM trzeci/emscripten:1.39.11-upstream

MAINTAINER esromneb


# build:
#
# docker build -t esromneb/qt-wasm/1.39.11:base base


ENV DEBIAN_FRONTEND noninteractive

RUN cd /root && git clone https://code.qt.io/qt/qt5.git && \
cd qt5 && git checkout 4c82f61c && \
git submodule update --init qtactiveqt qtcanvas3d qtcharts qtdatavis3d qtdeclarative qtdocgallery qtfeedback qtgamepad qtgraphicaleffects qtimageformats qtlottie qtmacextras qtnetworkauth qtpim qtpurchasing qtquick3d qtquickcontrols qtquickcontrols2 qtquicktimeline qtremoteobjects qtscript qtscxml qtsvg qtsystems qtvirtualkeyboard qtwebview qtxmlpatterns qtbase

RUN cd /root/qt5 && ./configure -no-optimized-qmake -no-optimize-debug -xplatform wasm-emscripten -nomake examples -skip qtconnectivity -skip qtlocation -skip qtmultimedia -skip qtsensors -skip qttools -skip qtwebsockets -skip qtwinextras -skip qtwebchannel -skip qtwebengine -skip qtspeech -skip qtsensors -skip qtserialbus -skip qtserialport  -nomake examples -nomake tests -opensource -confirm-license   -prefix $PWD/qtbase

RUN cd /root/qt5 && make -j4
