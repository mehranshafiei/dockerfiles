# syntax=docker/dockerfile:1
FROM ubuntu:18.04
RUN echo "Ubuntu"

# Get essential packages
RUN apt-get -y update
RUN apt-get -y install git build-essential libssl-dev ninja-build wget python3 libclang-dev libgl1-mesa-dev libglu1-mesa-dev
RUN apt-get -y install '^libxcb.*-dev' libx11-xcb-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev libclang-6.0-dev llvm-6.0

RUN bash
# Get, build and install cmake
RUN wget https://github.com/Kitware/CMake/releases/download/v3.20.2/cmake-3.20.2.tar.gz
RUN tar -zxvf cmake-3.20.2.tar.gz
RUN ./cmake-3.20.2/bootstrap
RUN cd cmake-3.20.2
RUN make -j 16
RUN make install
RUN rm -rf cmake-3.20.2

# Get, configure and build Qt5.15
RUN git clone https://github.com/qt/qt5.git
RUN cd qt5 && git checkout 5.15.2 && ./init-repository --module-subset=essential --force
RUN mkdir qt5-build && cd qt5-build && ../qt5/configure -developer-build -opensource -nomake examples -nomake tests -confirm-license -recheck-all -release -skip qtquick3d -prefix /opt/qt5.15.2 && make -j 16
