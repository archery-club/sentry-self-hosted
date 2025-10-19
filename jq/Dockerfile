FROM debian:bookworm-slim

LABEL MAINTAINER="oss@sentry.io"

RUN set -x \
  && echo "deb [trusted=yes] http://mirrors.aliyun.com/debian  bookworm main contrib non-free" > /etc/apt/sources.list  \
  && echo "deb [trusted=yes] http://mirrors.aliyun.com/debian  bookworm-updates main contrib non-free" >> /etc/apt/sources.list  \
  && echo "Acquire { https::Verify-Peer false }" >> /etc/apt/apt.conf.d/99verify-peer.conf \
  && apt-get update -y \
  && apt-get install -y gnupg \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 6ED0E7B82643E131 78DBA3BC47EF2265 \
  && apt-get update -y \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends jq \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["jq"]
