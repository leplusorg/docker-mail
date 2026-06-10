FROM alpine:3.24.0@sha256:a2d49ea686c2adfe3c992e47dc3b5e7fa6e6b5055609400dc2acaeb241c829f4

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-euo", "pipefail", "-c"]

RUN apk upgrade --no-cache \
    && apk add --no-cache \
    aspell=0.60.8.1-r0 \
    aspell-de=20161207.7.0-r0 \
    aspell-en=2020.12.07-r0 \
    aspell-fr=0.50.3-r0 \
    aspell-ru=0.99_p7-r2 \
    aspell-uk=1.4.0-r3 \
    coreutils=9.8-r1 \
    curl=8.19.0-r0 \
    git=2.52.0-r0 \
    mailutils=3.19-r0 \
    mutt=2.2.16-r0 \
    neomutt=20250905-r0 \
    notmuch=0.38.3-r1 \
    pipx=1.8.0-r0 \
    py3-pip=25.1.1-r1 \
    python3=3.12.13-r0 \
    && apk cache --no-cache clean \
    && rm -rf /var/cache/apk/*

COPY requirements.txt /tmp/requirements.txt

RUN pipx ensurepath --global \
    && xargs -a /tmp/requirements.txt -n 1 pipx install --global \
    && rm -f /tmp/requirements.txt

RUN adduser \
  --home "${USER_HOME}" \
  --uid "${USER_ID}" \
  --gecos "${USER_GECOS}" \
  --disabled-password \
  "${USER_NAME}"

USER "${USER_NAME}"

ENV HOME="${USER_HOME}"

WORKDIR "${HOME}"
