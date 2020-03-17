FROM ubuntu:bionic

MAINTAINER junior <ijuniorfu@gmail.com>

RUN mv /etc/apt/sources.list /etc/apt/sourses.list.bak
ADD sources.list /etc/apt/sources.list

# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update

RUN apt-get install -y software-properties-common \
    language-pack-en-base

RUN LC_ALL=en_US.UTF-8
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y curl wget git telnet cron supervisor vim net-tools
