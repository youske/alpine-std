# Alpine Linux standard

FROM alpine:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.geeplus.description="alpine standard image" \
      com.geeplus.vendor="geeplus.inc" \
      com.geeplus.role="baseimage"

ENV ENTRYKIT_VERSION=0.4.0
ENV ENTRYKIT_FILE=entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz
ENV ENTRYKIT_DOWNLOAD=https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/${ENTRYKIT_FILE}

ENV GOSU_VERSION=1.7
ENV GOSU_DOWNLOAD=https://github.com/tianon/gosu/releases/download/${GOSU_VERSION}/gosu-amd64

ENV PATH=$PATH \
    LANG=C.UTF-8 \
    WORK_DIR=/home/admin \
    PACKAGE='bash python ca-certificates' \
    BUILDPACK='wget build-base linux-headers'

RUN apk update --no-cache && apk add ${PACKAGE} --no-cache && apk add ${BUILDPACK} --no-cache -t buildpack

# entrykit install
RUN wget -q --no-check-certificate ${ENTRYKIT_DOWNLOAD} -O- | tar zx && \
    chmod +x /entrykit && mv /entrykit /bin && /bin/entrykit --symlink

# gosu
RUN wget -q --no-check-certificate ${GOSU_DOWNLOAD} -O /usr/bin/gosu && chmod +x /usr/bin/gosu

# remove
RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*

RUN adduser -D -h /home/admin -s /bin/bash admin admin

WORKDIR ${WORK_DIR}
CMD ["/usr/bash"]
