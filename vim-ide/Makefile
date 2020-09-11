NAME=vim-ide
BASE_DIR=$(HOME)/.dvim
UNDO_DIR=$(BASE_DIR)/undo
FTPLUGIN_DIR=$(BASE_DIR)/ftplugin
INST_DIR=/usr/local/bin
CONF_DIR=$(PWD)/configs
SNIPS_DIR=$(BASE_DIR)/ultisnips
OS=$(shell uname)

default: build
build:
	docker build --no-cache -t $(NAME) .
install:
	mkdir -p $(BASE_DIR)
	mkdir -p $(UNDO_DIR)
	mkdir -p $(FTPLUGIN_DIR)
	mkdir -p $(SNIPS_DIR)
	sudo cp dvim* $(INST_DIR)
	cp $(CONF_DIR)/dvimrc $(BASE_DIR)/dvimrc
	cp $(CONF_DIR)/coc-settings.json $(BASE_DIR)/coc-settings.json
	cp $(CONF_DIR)/pylintrc $(BASE_DIR)/pylintrc
	cp $(CONF_DIR)/pycodestyle $(BASE_DIR)/pycodestyle
	cp -rf $(CONF_DIR)/ultisnips/* $(BASE_DIR)/ultisnips
	xhost + local: > /dev/null || true
ifeq ($(OS),Darwin)
ifeq (,$(findstring coreutils, $(shell brew list)))
	brew install coreutils
endif
endif
clean:
	rm -f $(INST_DIR)/dvim*
	rm -rf $(BASE_DIR)
	docker rmi -f $(NAME)
