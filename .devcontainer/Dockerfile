FROM golang:1.16.2-alpine3.13

RUN apk add --no-cache \
        git \
        bash \
        build-base \
        openssh-client \
        bash-completion \
        git-bash-completion \
        sudo
    && mkdir -p /etc/skel \
    && touch /etc/skel/.bashrc \
    && echo "source /usr/share/bash-completion/completions/git" >> /etc/skel/.bashrc

ARG USERNAME
ARG USER_ID
ARG GROUP_ID

RUN addgroup -g ${GROUP_ID} ${USERNAME} \
    && adduser -S -D -u ${USER_ID} -G ${USERNAME} ${USERNAME} \
    && echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && cd /home/${USERNAME} \
    && mkdir -p -m0755 src \
    && echo "export PATH=\${HOME}/bin:\${PATH}" > .bashrc \
    && chown -R ${USER_ID}:${GROUP_ID} src .bashrc \
    && install -m 644 /dev/null .gitconfig
