FROM alpine:3.18
LABEL maintainer="Walber Vaz <wvs.walber@gmail.com>"

ARG USER=app
ARG PY_VERSION=3.11.4
ENV HOME /home/$USER

RUN apk update \
  && apk upgrade --no-cache -i \
  && apk add --no-cache \
    sudo \
    bash \
    git \
    curl \
    wget \
    build-base \
    libffi-dev \
    openssl-dev \
    bzip2-dev \
    zlib-dev \
    xz-dev \
    readline-dev \
    sqlite-dev \
    tk-dev \
    linux-headers -i \
  && rm -rf /var/cache/apk/* \
  && rm -rf /tmp/* \
  && sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

RUN addgroup -S $USER \
  && adduser -S $USER -G $USER -h $HOME -s /bin/bash \
  && mkdir -p /etc/sudoers.d \
  && echo "$USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USER \
  && chmod 0440 /etc/sudoers.d/$USER

USER $USER
WORKDIR $HOME

# instalar pyenv
RUN mkdir -p $HOME/.local/bin \
  && git clone https://github.com/pyenv/pyenv.git $HOME/.pyenv

ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$HOME/.local/bin:$PATH

# instalar python
RUN pyenv install $PY_VERSION
RUN pyenv global $PY_VERSION
RUN pyenv rehash

# instalar pip
RUN pip install --upgrade pip --no-cache-dir \
  && pip install --upgrade setuptools --no-cache-dir \
  && pip install --upgrade wheel --no-cache-dir

RUN curl -sSL https://install.python-poetry.org | python3 -
