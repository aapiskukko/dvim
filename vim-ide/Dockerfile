FROM vim-basic:latest

RUN \
    # Add edge repository
    echo http://nl.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories \
    # Download and install required install deps
    && apk add --no-cache --update \
        build-base \
        git \
        bash \
        curl \
        libxml2-utils \
        nodejs \
        yarn \
        npm \
        the_silver_searcher \
        ctags \
        file \
        clang \
        clang-extra-tools \
        ccls \
    && pip install --upgrade --no-cache-dir \
        six \
        pyls-black \
        isort \
        pynvim \
    && git clone https://github.com/junegunn/fzf.git /root/.fzf \
    && /root/.fzf/install \
    # Install syntax related plugins
    && mkdir -p /root/.vim/pack/syntax/start \
    && cd /root/.vim/pack/syntax/start \
    && git clone https://github.com/andymass/vim-matchup.git \
    #&& git clone https://github.com/w0rp/ale.git \
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
    && git clone https://github.com/tpope/vim-obsession.git \
    && git clone https://github.com/tpope/vim-surround.git \
    && git clone https://github.com/mjbrownie/swapit.git \
    && git clone https://github.com/vim-scripts/a.vim.git \
    # Remove build packages
    #&& apk del \
    #   build-base \
    # Remove unused files
    && rm -rf \
        /var/log/* \
        var/tmp/* \
        /tmp/*

RUN mkdir -p /root/ctags/proj /root/.config
COPY configs/bashrc /root/.bashrc
RUN \
    mkdir -p /root/.vim/pack/syntax/start \
    && cd /root/.vim/pack/syntax/start \
    && curl --fail -L https://github.com/neoclide/coc.nvim/archive/release.tar.gz | tar xzfv -
RUN \
    mkdir -p /root/.config/coc/extensions \
    && cd /root/.config/coc/extensions \
    && echo '{"dependencies":{}}'> package.json \
    && npm install --global-style --ignore-scripts --no-bin-links --no-package-lock --only=prod \
         coc-pyright \
         coc-tsserver \
         coc-json \
         coc-docker \
         coc-snippets \
         coc-cmake \
         coc-git \
         coc-sql \
         coc-fzf-preview \
         coc-clangd
