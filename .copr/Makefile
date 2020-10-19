VERSION := $(shell cat $(dir $(spec))VERSION)

$(spec): $(spec).in
	sed "s|@VERSION@|$(VERSION)|g" $(spec).in > $(spec)

srpm: $(spec)
	rpmbuild --undefine "_disable_source_fetch" \
	         --define "_srcrpmdir $(outdir)" \
	         --rmsource \
	         -bs $(spec)

.PHONY: spec srpm
