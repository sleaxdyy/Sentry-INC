ARG SENTRY_IMAGE
FROM ${SENTRY_IMAGE}

COPY . /usr/src/sentry

ADD pip.conf /etc/pip.conf

RUN rm -rf /etc/apt/sources.list.d
RUN echo "deb [trusted=yes] https://registry.example.com/repository/deb-debian-12-proxy/ bookworm main" > /etc/apt/sources.list
RUN echo "Acquire { https::Verify-Peer false }" > /etc/apt/apt.conf.d/99verify-peer.conf

RUN apt-get update
RUN apt-get install -y gcc libsasl2-dev python-dev-is-python3 libldap2-dev libssl-dev

RUN pip install hvac
RUN pip install requests
RUN pip install sentry_auth_ldap
RUN pip install django-auth-ldap
RUN pip install python-dotenv

RUN if [ -s /usr/src/sentry/enhance-image.sh ]; then \
    /usr/src/sentry/enhance-image.sh; \
fi

RUN chown -R sentry:sentry /usr/src/sentry
RUN chown -R sentry:sentry /root
RUN chown -R sentry:sentry /etc/ssl

USER sentry
