this_dir := $(abspath $(dir $(lastword $(MAKEFILE_LIST))))

TOP_DIR  ?= $(abspath $(this_dir)/..)

OUTPUT_DIR := $(TOP_DIR)/build


.PHONY: all
all: build install

.PHONY: build
build:
	@true

.PHONY: install
install:
	@mkdir -p $(OUTPUT_DIR)
	@tar -C .. -cf $(OUTPUT_DIR)/for-qt-noVNC.tar app core vnc.html AUTHORS LICENSE.txt package.json vendor vnc_lite.html

.PHONY: clean
clean:
	@rm -rf $(OUTPUT_DIR)

