FROM trzeci/emscripten:1.39.10-upstream

MAINTAINER esromneb


# build:
#
# docker build -t esromneb/qt-wasm/1.39.11:base base


ENV DEBIAN_FRONTEND noninteractive

USER emscripten

RUN cd ~ && git clone https://code.qt.io/qt/qt5.git && \
cd qt5 && git checkout 09d23573 && \
git submodule update --init qtactiveqt qtcanvas3d qtcharts qtdatavis3d qtdeclarative qtdocgallery qtfeedback qtgamepad qtgraphicaleffects qtimageformats qtlottie qtmacextras qtnetworkauth qtpim qtpurchasing qtquick3d qtquickcontrols qtquickcontrols2 qtquicktimeline qtremoteobjects qtscript qtscxml qtsvg qtsystems qtvirtualkeyboard qtwebview qtxmlpatterns qtbase

# I set fPIC according to https://bugreports.qt.io/browse/QTBUG-58511?page=com.googlecode.jira-suite-utilities%3Atransitions-summary-tabpanel
# It's possible I don't need it anymore with new qmake compile approach

RUN cd ~/qt5 && ./configure QMAKE_CXXFLAGS=-fPIC -no-optimized-qmake -no-optimize-debug --disable-shared -xplatform wasm-emscripten -nomake examples -skip qtconnectivity -skip qtlocation -skip qtmultimedia -skip qtsensors -skip qttools -skip qtwebsockets -skip qtwinextras -skip qtwebchannel -skip qtwebengine -skip qtspeech -skip qtsensors -skip qtserialbus -skip qtserialport  -nomake examples -nomake tests -opensource -confirm-license   -prefix $PWD/qtbase

RUN cd ~/qt5 && make -j4

ENV PATH "$PATH:/home/emscripten/qt5/qtbase/bin/"

