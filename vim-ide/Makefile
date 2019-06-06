NAME=vim-ide
BASE_DIR=.dvim
UNDO_DIR=$(HOME)/$(BASE_DIR)/undo
FTPLUGIN_DIR=$(HOME)/$(BASE_DIR)/ftplugin
INST_DIR="/usr/local/bin"
OS=$(shell uname)

default: build
build:
	docker build --no-cache -t $(NAME) .
install:
	mkdir -p $(UNDO_DIR)
	mkdir -p $(FTPLUGIN_DIR)
	sudo cp dvim* $(INST_DIR)
ifeq ($(OS),Darwin)
ifeq (,$(findstring coreutils, $(shell brew list)))
	brew install coreutils
endif
endif
clean:
	rm -f $(INST_DIR)/dvim*
	docker rmi -f $(NAME)
