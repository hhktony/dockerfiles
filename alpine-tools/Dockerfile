# build: docker build -t hhktony/tools:1.0 .
# test: docker run --rm -it --privileged -v /run:/run --net=host hhktony/tools:1.0 bash
FROM alpine:3.16
MAINTAINER Tony Xu <hhktony@gmail.com>

# RUN [ ! -e /etc/nsswitch.conf ] && echo 'hosts: files dns' > /etc/nsswitch.conf
RUN sed -i 's/dl-cdn.alpinelinux.org/mirror.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
    && apk update \
    && apk add tzdata \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk add busybox-extras bash bash-completion tmux \
               sysstat htop iftop curl mtr iproute2 iputils netcat-openbsd socat tcpdump conntrack-tools \
    && rm -rf /var/cache/apk/* \
    && echo "export PS1='C \u@\h:\W \\$ '" > /root/.bashrc \
    && echo "source /etc/profile.d/bash_completion.sh" >> /root/.bashrc \
    && sed -i 's|ash|bash|g' /etc/passwd

LABEL name="tools" description="Tools" \
      tools.cmd="docker run --rm -it --privileged -v /run:/run --net=host hhktony/tools:1.0 bash"

ENTRYPOINT ["sleep", "infinity"]
