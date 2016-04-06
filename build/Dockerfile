# Alpine Linux standard
# alpine based

FROM alpine:latest
MAINTAINER youske miyakoshi <youske@gmail.com>

ENV ENTRYKIT_VERSION=0.4.0
ENV ENTRYKIT_FILE=entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz
ENV ENTRYKIT_DOWNLOAD=https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/${ENTRYKIT_FILE}

ENV PATH=$PATH \
    LANG=C.UTF-8 \
    WORK_DIR=/home/admin \
    PACKAGE='bash python ' \
    BUILDPACK='wget ca-certificates'

#libstdc++

RUN apk add ${PACKAGE} --no-cache && apk add ${BUILDPACK} --no-cache -t buildpack

# entrykit install
RUN wget -q --no-check-certificate ${ENTRYKIT_DOWNLOAD} -O- | tar zx && \
    chmod +x /entrykit && mv /entrykit /bin && /bin/entrykit --symlink

RUN apk del buildpack --no-cache && rm -rf /tmp/* /var/cache/apk/*

RUN adduser -D -h /home/admin -s /bin/bash admin admin

WORKDIR ${WORK_DIR}
CMD ["bash"]
