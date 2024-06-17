FROM ubuntu:24.04 as BUILDER
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
  && apt-get install -y ca-certificates
RUN sed -i "s@http://.*security.ubuntu.com@https://mirrors.ustc.edu.cn@g" /etc/apt/sources.list.d/ubuntu.sources \
  && sed -i "s@http://.*archive.ubuntu.com@https://mirrors.ustc.edu.cn@g" /etc/apt/sources.list.d/ubuntu.sources
RUN apt-get update \
  && apt-get install -y build-essential cmake gdb clang \
  && apt-get clean
WORKDIR /app
COPY . /app
RUN cmake . -B build \
  && cmake --build build
