FROM fedora:25
MAINTAINER David Wagner <david.wagner@easymile.com>

RUN echo "fastestmirror=True" >> /etc/dnf/dnf.conf

RUN dnf install -y \
    git \
    gcc-c++ \
    cmake \
    make \
    gstreamer1-rtsp-server-devel \
    gstreamer1-plugins-good \
    boost-program-options \
    boost-devel \
    catch-devel

RUN adduser -Um user
USER user
WORKDIR /home/user

RUN git clone https://github.com/EasyMile/ez-rtsp-server.git
WORKDIR ez-rtsp-server
RUN git checkout 6ae2edd3b2760be56b211d758fd330fcf7856a0d

RUN mkdir ../build
WORKDIR ../build
RUN cmake ../ez-rtsp-server && make

ENTRYPOINT ["./SimpleRtspServer", "--port", "8554"]
EXPOSE 8554
