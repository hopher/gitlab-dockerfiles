FROM gitlab/gitlab-ce:latest
LABEL maintainer="hopher <565983236@qq.com>"

# 设置时区
ENV TIMEZONE=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo $TIMEZONE > /etc/timezone

# 设置安装源镜像
ENV MIRROR_SOURCE=tencent
COPY ./mirrors/$MIRROR_SOURCE/ubuntu/ubuntu16_sources.list /etc/apt/sources.list