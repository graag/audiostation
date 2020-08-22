FROM alpine:3

WORKDIR /data
ARG SNAPCASTVERSION=v0.20.0

RUN apk -U add git bash build-base asio-dev avahi-dev flac-dev libvorbis-dev alsa-lib-dev soxr-dev opus-dev \
  && cd /root \
  && git clone --recursive https://github.com/badaix/snapcast.git \
  && cd snapcast \
  && git checkout tags/${SNAPCASTVERSION} -b ${SNAPCASTVERSION} \
  && cd externals \
  && git submodule update --init --recursive \
  && cd - \
  && make \
  && cp server/snapserver client/snapclient /usr/local/bin \
  && cd / \
  && apk --purge del git bash build-base asio-dev bash avahi-dev flac-dev libvorbis-dev alsa-lib-dev soxr-dev opus-dev \
  && apk add avahi-libs flac libvorbis alsa-lib opus soxr \
  && rm -rf /etc/ssl /var/cache/apk/* /lib/apk/db/* /root/snapcast

ADD snapserver.conf /etc/snapserver.conf
CMD ["snapserver"]
