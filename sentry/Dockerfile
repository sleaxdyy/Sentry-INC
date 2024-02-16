ARG SENTRY_IMAGE
FROM ${SENTRY_IMAGE}

COPY . /usr/src/sentry

RUN apt-get update
RUN apt-get install -y gcc libsasl2-dev python-dev libldap2-dev libssl-dev

RUN pip install hvac
RUN pip install requests
RUN pip install sentry_auth_ldap
RUN pip install django-auth-ldap
RUN pip install python-dotenv


RUN if [ -s /usr/src/sentry/enhance-image.sh ]; then \
    /usr/src/sentry/enhance-image.sh; \
fi

RUN if [ -s /usr/src/sentry/requirements.txt ]; then \
    echo "sentry/requirements.txt is deprecated, use sentry/enhance-image.sh - see https://github.com/getsentry/self-hosted#enhance-sentry-image"; \
    pip install -r /usr/src/sentry/requirements.txt; \
fi

RUN chown -R sentry:sentry /usr/src/sentry
RUN chown -R sentry:sentry /root
RUN chown -R sentry:sentry /etc/ssl

USER sentry
