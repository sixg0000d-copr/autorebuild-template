MAKEFILE_PATH := $(abspath $(lastword $(MAKEFILE_LIST)))
DOT_COPR_PATH := $(dir $(MAKEFILE_PATH))
export REPO_ROOT := $(abspath $(DOT_COPR_PATH)/..)
export REPO_NAME := $(notdir $(REPO_ROOT))

VERSION := $(shell cat $(REPO_ROOT)/VERSION)

spec ?= $(REPO_ROOT)/$(REPO_NAME).spec
outdir ?= $(REPO_ROOT)

default: srpm

HAS_GIT := $(shell command -v git 2>/dev/null)
ifndef HAS_GIT
git-core:
	dnf -y install git-core
else
git-core:
endif

$(spec): $(spec).in
	sed "s|@VERSION@|$(VERSION)|g" $(spec).in > $(spec)

spec: $(spec)

srpm: spec
	rpmbuild --undefine "_disable_source_fetch" \
	         --define "_srcrpmdir $(outdir)" \
	         --rmsource \
	         -bs $(spec)

clean: git-core
	git clean -xdf

.PHONY: default git-core spec srpm clean
