From vim-basic:latest
MAINTAINER Aatu Koivisto <aatukoivi@gmail.com>

RUN \
    # Add edge repository
    echo http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
    # Download and install required install deps
    && apk add --no-cache --update \
        git \
        automake \
        autoconf \
        build-base \
        pkgconfig \
    && apk add --no-cache \
        python \
        python3 \
        py-pip \
        bash \
        curl \
        libxml2-utils \
        nodejs \
        yarn \
        the_silver_searcher \
    && pip install --upgrade --no-cache-dir \
        pip \
        six \
        setuptools \
        jedi \
        yapf \
        pylint \
        pycodestyle \
        rope \
        python-language-server \
        requests \
    # Install fzf
    && git clone https://github.com/junegunn/fzf.git /root/.fzf \
    && /root/.fzf/install \
    # Install universal-ctags
    && cd /tmp \
    && git clone https://github.com/universal-ctags/ctags.git \
    && cd /tmp/ctags \
    && ./autogen.sh \
    && ./configure --prefix=/usr \
    && make -j$(nproc) install \
    # Install syntax related plugins
    && mkdir -p /root/.vim/pack/syntax/start \
    && cd /root/.vim/pack/syntax/start \
    && git clone https://github.com/andymass/vim-matchup.git \
    && git clone https://github.com/neoclide/coc.nvim.git \
    # Install outfit related plugins
    && mkdir -p /root/.vim/pack/looks/start \
    && cd /root/.vim/pack/looks/start \
    && git clone https://github.com/nanotech/jellybeans.vim.git \
    && git clone https://github.com/vim-airline/vim-airline.git \
    && git clone https://github.com/vim-airline/vim-airline-themes.git \
    && git clone https://github.com/octol/vim-cpp-enhanced-highlight.git \
    # Install util plugins
    && mkdir -p /root/.vim/pack/util/start \
    && cd /root/.vim/pack/util/start \
    && git clone https://github.com/junegunn/fzf.vim.git \
    && git clone https://github.com/scrooloose/nerdcommenter.git \
    && git clone https://github.com/SirVer/ultisnips.git \
    && git clone https://github.com/tpope/vim-obsession.git \
    && git clone https://github.com/tpope/vim-surround.git \
    && git clone https://github.com/mjbrownie/swapit.git \
    && git clone https://github.com/vim-scripts/a.vim.git \
    # Remove build packages
    && apk del \
        git \
        build-base \
        autoconf \
        automake \
        pkgconfig \
    # Remove unused files
    && rm -rf \
        /var/cache/apk/* \
        /var/log/* \
        var/tmp/* \
        /tmp/*

RUN mkdir -p /root/ctags/proj /root/.config
COPY bashrc /root/.bashrc
COPY pycodestyle /root/.config/pycodestyle
RUN \
    cd /root/.vim/pack/syntax/start/coc.nvim \
    && ./install.sh
RUN \
    mkdir -p /root/.config/coc/extensions \
    && cd /root/.config/coc/extensions \
    && yarn add coc-python coc-tsserver
