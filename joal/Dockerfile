ARG BUILD_FROM
ARG BUILD_UPSTREAM="2.1.26"
FROM anthonyraymond/joal:$BUILD_UPSTREAM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ARG BUILD_VERSION
ARG BUILD_UPSTREAM="2.1.26"

RUN \
#Install bashio
    apt-get clean \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
    wget \
    jq \
    nginx \
#Install bashio
    && curl -J -L -o /tmp/bashio.tar.gz \
    "https://github.com/hassio-addons/bashio/archive/v0.13.1.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf \
    /tmp/bashio.tar.gz \
    --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    \
#Install Joal
    && wget -O /tmp/joal.tar.gz "https://github.com/anthonyraymond/joal/releases/download/$BUILD_UPSTREAM/joal.tar.gz" \
    && mkdir -p /data/joal \
    && tar zxvf /tmp/joal.tar.gz -C /data/joal \
    && rm /data/joal/jack-of* \
#Clean
    && rm -fr \
    /tmp/* \
    /var/{cache,log}/* \
    /var/lib/apt/lists/*

VOLUME [ "/data" ]

# Copy root filesystem
COPY rootfs / 
RUN chmod 777 /run.sh

ENTRYPOINT [ "/run.sh" ]
