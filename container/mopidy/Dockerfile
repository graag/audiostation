FROM alpine:3.18

RUN mkdir /etc/default && mkdir /etc/mopidy

RUN apk update \
  && apk upgrade \
  && apk add mopidy
#  && apk add --no-cache \
#  --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing \
#  mopidy

# I cant explain why, but to me it seems
# I have less pause in streams if I
# also install these. However image size
# also grows by about 80MB
#RUN apk add --no-cache \
#  gst-plugins-base0.10 \
#  gst-plugins-good0.10 \
#  gst-plugins-ugly0.10 \
#  py-gst0.10

## Install Pip to install extensions
RUN apk add --no-cache \
  py-pip \
  && pip install --upgrade pip

## Install extensions
RUN pip install -U Mopidy-MusicBox-Webclient \
  && pip install -U Mopidy-MPD \
  && pip install -U Mopidy-Local

# Workaround for GStreamer error
COPY mopidy/mopidy/audio/actor.py /usr/lib/python3.11/site-packages/mopidy/audio/actor.py

##  Copy fallback configuration.
COPY mopidy.conf /etc/default/mopidy.conf

#  Copy default configuration.
COPY mopidy.conf /etc/mopidy/mopidy.conf

# Copy helper script.
COPY entrypoint.sh /entrypoint.sh

VOLUME ["/data", "/cache"]

EXPOSE 6600 6680 5555/udp

ENTRYPOINT ["/entrypoint.sh"]
