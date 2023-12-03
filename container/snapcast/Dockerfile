FROM alpine:3

RUN apk -U add snapcast

ADD snapserver.conf /etc/snapserver.conf
CMD ["snapserver"]
