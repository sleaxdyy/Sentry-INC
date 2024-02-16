FROM debian:bookworm-slim
RUN rm -rf /etc/apt/sources.list.d
RUN echo "deb [trusted=yes] https://registry.example.com/repository/deb-debian-12-proxy/ bookworm main" > /etc/apt/sources.list
RUN echo "Acquire {https: :Verify-Peer false }" > /etc/apt/apt.conf.d/99verify-peer.conf
RUN apt-get update
RUN apt reinstall ca-certificates -y
RUN apt-get update
RUN apt install -y jq
RUN rm -rf /etc/apt/apt.conf.d/99verify-peer.conf
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
USER sentry
ENTRYPOINT ["jq"]
