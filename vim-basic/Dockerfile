FROM python:3.9-alpine

RUN \
    # Download and install required install deps
    apk add --no-cache --update --virtual \
        build-deps \
        python3-dev \
        build-base \
        git \
        ncurses-dev \
        libx11-dev \
        libxpm-dev \
        libxt-dev \
        make \
        lua-dev \
    # Download and install Vim
    && cd /tmp \
    && git clone https://github.com/vim/vim.git \
    && cd /tmp/vim \
    && ./configure \
        --enable-pythoninterp \
        --enable-luainterp \
        --with-features=huge \
        --with-x \
        --disable-gui \
        --prefix=/usr \
    && make -j$(nproc) install \
    # Add vimrc
    && cd /tmp \
    # Remove build packages
    && apk del \
        build-base \
        build-deps \
        git \
        make \
    # Add required non-dev packages
    && apk add \
        ncurses \
        libice \
        libsm \
        libx11 \
        libxt \
        diffutils \
        lua \
    # Remove unused files
    && rm -rf \
        /var/cache/apk/* \
        /var/log/* \
        var/tmp/* \
        /tmp/*
