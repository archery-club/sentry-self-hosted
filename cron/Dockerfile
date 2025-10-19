ARG BASE_IMAGE
FROM ${BASE_IMAGE}
USER 0
RUN if [ -n "${HTTP_PROXY}" ]; then echo "Acquire::http::proxy \"${HTTP_PROXY}\";" >> /etc/apt/apt.conf; fi
RUN if [ -n "${HTTPS_PROXY}" ]; then echo "Acquire::https::proxy \"${HTTPS_PROXY}\";" >> /etc/apt/apt.conf; fi
RUN if [ -n "${http_proxy}" ]; then echo "Acquire::http::proxy \"${http_proxy}\";" >> /etc/apt/apt.conf; fi
RUN if [ -n "${https_proxy}" ]; then echo "Acquire::https::proxy \"${https_proxy}\";" >> /etc/apt/apt.conf; fi
RUN set -x \
  && echo "deb [trusted=yes] http://mirrors.aliyun.com/debian  bookworm main contrib non-free" > /etc/apt/sources.list  \
  && echo "deb [trusted=yes] http://mirrors.aliyun.com/debian  bookworm-updates main contrib non-free" >> /etc/apt/sources.list  \
  && echo "Acquire { https::Verify-Peer false }" >> /etc/apt/apt.conf.d/99verify-peer.conf \
  && apt-get update -y \
  && apt-get install -y gnupg \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 6ED0E7B82643E131 78DBA3BC47EF2265
RUN apt-get update && apt-get install -y --no-install-recommends cron && \
    rm -r /var/lib/apt/lists/*
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
