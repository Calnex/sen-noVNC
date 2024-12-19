MAKEFLAGS += --no-print-directory
Q=@

.DEFAULT_GOAL := all
.PHONY: all clean 

this_dir := $(abspath $(dir $(lastword $(MAKEFILE_LIST))))

TOP_DIR  ?= $(abspath $(this_dir)/..)

OUTPUT_DIR := $(TOP_DIR)/build

NO_VNC_VERSION := $(shell cat $(TOP_DIR)/package.json | jq -r '.version')

include version

VERSION=$(NO_VNC_VERSION).$(CALNEX_VERSION)
VERSION_FILE=$(OUTPUT_DIR)/version

APP_FILES := $(shell find $(TOP_DIR)/app -type f)
CORE_FILES := $(shell find $(TOP_DIR)/core -type f)
VENDOR_FILES := $(shell find $(TOP_DIR)/vendor -type f)
ADDITIONAL_FILES := $(TOP_DIR)/vnc.html \
                    $(TOP_DIR)/AUTHORS \
					$(TOP_DIR)/LICENSE.txt \
					$(TOP_DIR)/package.json \
					$(TOP_DIR)/vnc_lite.html

OUTPUT=$(OUTPUT_DIR)/noVNC-calnex-$(VERSION).tar

all: $(OUTPUT)
	@true

$(OUTPUT) : $(APP_FILES) $(CORE_FILES) $(ADDITIONAL_FILES) $(VERSION_FILE)
	$(Q)mkdir -p $(OUTPUT_DIR)
	@printf "Build   - %s\n" "$@"
	$(Q)tar -C $(TOP_DIR) -Pcf $@ app core vendor $(notdir $(ADDITIONAL_FILES)) $(VERSION_FILE) --transform 's,^.*/build/,,'

$(VERSION_FILE) : $(TOP_DIR)/calnex/version $(TOP_DIR)/package.json
	$(Q)mkdir -p $(OUTPUT_DIR)
	@printf "Create  - Version File %s\n" "$@"
	@echo $(VERSION) > $@

clean:
	@printf "Clean   - %s\n" "$(OUTPUT_DIR)"
	$(Q)rm -rf $(OUTPUT_DIR)

