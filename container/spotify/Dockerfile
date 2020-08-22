FROM debian:buster-slim
MAINTAINER Malte Deiseroth <mdeiseroth88@gmail.com>
ARG VERSION=v0.2.24

RUN apt-get update -qq \
 && apt-get install -yqq libasound2 libvorbisfile3 tar wget \
 && wget -O /tmp/spotifyd.tar.gz https://github.com/Spotifyd/spotifyd/releases/download/$VERSION/spotifyd-linux-slim.tar.gz \
 && tar -C /usr/bin -x -z -f /tmp/spotifyd.tar.gz \
 && apt-get remove -y --purge unzip wget \
 && apt-get autoremove -y \
 && rm /tmp/*.tar.gz

ADD entrypoint.sh /usr/bin
ADD spotifyd.conf /etc/spotifyd.conf
ADD asound.conf /etc/asound.conf

CMD ["/usr/bin/entrypoint.sh"]
