TOOLSBIN = $(MARSDEV)/bin

SJASM     = $(TOOLSBIN)/sjasm
SJBRANCH ?= v0.39

# Use homebrew's gettext on macOS, for autopoint
ifeq ($(OS),Windows_NT)
else
	UNAME_S := $(shell uname -s)
	ifeq ($(UNAME_S),Darwin)
		export PATH := /usr/local/opt/gettext/bin:$(PATH)
	endif
endif

# OSX sed fails without the '', and GNU fails with, coolbeans
SED_FIX=
ifeq ($(shell uname -s),Darwin)
	SED_FIX=''
endif

.PHONY: all clean

all: $(SJASM)

$(SJASM): $(TOOLSBIN)
	rm -rf sjasm
	git clone https://github.com/konamiman/sjasm --branch $(SJBRANCH)
	cd sjasm/Sjasm && $(MAKE)
	cp -f sjasm/Sjasm/sjasm $(SJASM)

$(TOOLSBIN):
	mkdir -p $(TOOLSBIN)

clean:
	rm -rf sjasm
