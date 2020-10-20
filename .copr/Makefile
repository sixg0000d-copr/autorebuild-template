MAKEFILE_PATH := $(abspath $(lastword $(MAKEFILE_LIST)))
MAKEFILE_DIR_PATH := $(dir $(MAKEFILE_PATH))
export REPO_ROOT := $(realpath $(MAKEFILE_DIR_PATH)/..)

VERSION := $(shell cat $(REPO_ROOT)/VERSION)

SPEC := $(or $(spec), $(REPO_ROOT)/template.spec)
OUTDIR := $(or $(outdir), $(REPO_ROOT))

default: srpm

HAS_GIT := $(shell command -v git 2>/dev/null)
ifndef HAS_GIT
git-core:
	dnf -y install git-core
else
git-core:
endif

$(SPEC): $(SPEC).in
	sed "s|@VERSION@|$(VERSION)|g" $(SPEC).in > $(SPEC)

spec: $(SPEC)

srpm: spec
	rpmbuild --undefine "_disable_source_fetch" \
	         --define "_srcrpmdir $(OUTDIR)" \
	         --rmsource \
	         -bs $(SPEC)

clean: git-core
	git clean -xdf

.PHONY: default git-core spec srpm clean
