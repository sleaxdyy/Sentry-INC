ARG BASE_IMAGE 
FROM ${BASE_IMAGE}
USER 0
RUN if [ -z "${http_proxy}" ]; then echo "Acquire::http::proxy \"${http_proxy}\";" >> /etc/apt/apt.conf; fi
RUN if [ -z "${https_proxy}" ]; then echo "Acquire::https::proxy \"${https_proxy}\";" >> /etc/apt/apt.conf; fi
RUN rm -rf /etc/apt/sources.list.d
RUN echo "deb [trusted=yes] https://registry.example.com/repository/deb-debian-12-proxy/ bookworm main" > /etc/apt/sources.list
RUN echo "Acquire { https::Verify-Peer false }" > /etc/apt/apt.conf.d/99verify-peer.conf
RUN apt-get update
RUN apt reinstall ca-certificates -y
RUN apt-get update
RUN apt install -y cron
RUN rm -rf /etc/apt/apt.conf.d/99verify-peer.conf
RUN rm -rf /var/lib/apt/lists/*
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
