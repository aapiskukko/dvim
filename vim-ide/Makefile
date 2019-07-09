NAME=vim-ide
BASE_DIR=.dvim
UNDO_DIR=$(HOME)/$(BASE_DIR)/undo
FTPLUGIN_DIR=$(HOME)/$(BASE_DIR)/ftplugin
INST_DIR="/usr/local/bin"
DVIM_CONF="configs/dvimrc"
COC_CONF="$(PWD)/configs/coc-settings.json"
PYLINT_CONF="$(PWD)/configs/pylintrc"
PYCODES_CONF="$(PWD)/configs/pycodestyle"
OS=$(shell uname)

default: build
build:
	docker build --no-cache -t $(NAME) .
install:
	mkdir -p $(UNDO_DIR)
	mkdir -p $(FTPLUGIN_DIR)
	sudo cp dvim* $(INST_DIR)
	cp $(COC_CONF) $(HOME)/$(BASE_DIR)
	cp $(PYLINT_CONF) $(HOME)/$(BASE_DIR)
	cp $(DVIM_CONF) $(HOME)/$(BASE_DIR)
	cp $(PYCODES_CONF) $(HOME)/$(BASE_DIR)
ifeq ($(OS),Darwin)
ifeq (,$(findstring coreutils, $(shell brew list)))
	brew install coreutils
endif
endif
clean:
	rm -f $(INST_DIR)/dvim*
	docker rmi -f $(NAME)
