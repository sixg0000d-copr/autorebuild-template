MAKEFILE_PATH := $(abspath $(lastword $(MAKEFILE_LIST)))
DOT_COPR_PATH := $(dir $(MAKEFILE_PATH))
PROJECT_REPO_ROOT := $(abspath $(DOT_COPR_PATH)/..)
PROJECT_NAME := $(notdir $(PROJECT_REPO_ROOT))
SOURCE_NAME := $(PROJECT_NAME)

spec := $(or $(spec), $(PROJECT_REPO_ROOT)/$(PROJECT_NAME).spec)
outdir := $(or $(outdir), $(PWD))

VERSION := $(shell cat $(PROJECT_REPO_ROOT)/VERSION)

default: srpm

spec: $(spec).in
	sed -e "s|@VERSION@|$(VERSION)|g" $(spec).in > $(spec)

source: runtime-deps spec
	spectool --get-files \
			 --directory=$(outdir) \
			 $(spec)

srpm: spec source
	rpmbuild --define "_sourcedir $(outdir)" \
	         --define "_srcrpmdir $(outdir)" \
			 -bs $(spec)

runtime-deps:
	dnf install -y "rpmdevtools"

clean:
	rm -rf $(spec) \
	       $(outdir)/$(SOURCE_NAME)-$(VERSION).tar.gz \
		   $(outdir)/$(PROJECT_NAME)-$(VERSION).rpm

.PHONY: default spec source srpm runtime-deps clean
