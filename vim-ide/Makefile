NAME=vim-ide
BASE_DIR=.dvim
UNDO_DIR=$(HOME)/$(BASE_DIR)/undo
FTPLUGIN_DIR=$(HOME)/$(BASE_DIR)/ftplugin
INST_DIR=/usr/local/bin
CONF_DIR=$(PWD)/configs
OS=$(shell uname)

default: build
build:
	docker build --no-cache -t $(NAME) .
install:
	mkdir -p $(UNDO_DIR)
	mkdir -p $(FTPLUGIN_DIR)
	sudo cp dvim* $(INST_DIR)
	cp $(CONF_DIR)/dvimrc $(HOME)/$(BASE_DIR)/dvimrc
	cp $(CONF_DIR)/coc-settings.json $(HOME)/$(BASE_DIR)/coc-settings.json
	cp $(CONF_DIR)/pylintrc $(HOME)/$(BASE_DIR)/pylintrc
	cp $(CONF_DIR)/pycodestyle $(HOME)/$(BASE_DIR)/pycodestyle
ifeq ($(OS),Darwin)
ifeq (,$(findstring coreutils, $(shell brew list)))
	brew install coreutils
endif
endif
clean:
	rm -f $(INST_DIR)/dvim*
	rm -rf $(HOME)/$(BASE_DIR)
	docker rmi -f $(NAME)
