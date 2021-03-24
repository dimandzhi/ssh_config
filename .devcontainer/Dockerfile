FROM golang:1.16.2-alpine3.13

RUN apk add --no-cache \
        git \
        bash \
        build-base \
        openssh-client \
        bash-completion \
        git-bash-completion \
        sudo

ARG USERNAME
ARG USER_ID
ARG GROUP_ID

RUN addgroup -g ${GROUP_ID} ${USERNAME} \
    && adduser -S -D -u ${USER_ID} -G ${USERNAME} ${USERNAME} \
    && echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && cd /home/${USERNAME} \
    && mkdir -p -m0755 src \
    && chown -R ${USER_ID}:${GROUP_ID} src
