FROM alpine:3.24.1@sha256:28bd5fe8b56d1bd048e5babf5b10710ebe0bae67db86916198a6eec434943f8b

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-euo", "pipefail", "-c"]

RUN apk upgrade --no-cache \
    && apk add --no-cache \
    aspell=0.60.8.2-r0 \
    aspell-de=20161207.7.0-r0 \
    aspell-en=2026.02.25-r0 \
    aspell-fr=0.50.3-r0 \
    aspell-ru=0.99_p7-r2 \
    aspell-uk=1.4.0-r3 \
    coreutils=9.11-r0 \
    curl=8.21.0-r0 \
    git=2.54.0-r0 \
    mailutils=3.21-r1 \
    mutt=2.3.2-r0 \
    neomutt=20260504-r0 \
    notmuch=0.40-r2 \
    pipx=1.14.0-r0 \
    py3-pip=26.1.2-r0 \
    python3=3.14.5-r0 \
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
