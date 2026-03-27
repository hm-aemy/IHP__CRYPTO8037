WORK_DIR=$(shell pwd)
TOP=top
TAG=top-run

PDK_ROOT ?= $(WORK_DIR)/../../../../pdk
PDK = ihp-sg13cmos5l

.PHONY: librelane
librelane:
	PDK_ROOT=$(PDK_ROOT) PDK=$(PDK) librelane --manual-pdk --run-tag $(TAG) --overwrite config.yaml
	rm -rf final
	cp -r runs/$(TAG)/final final

.PHONY: librelane-to-sealring
librelane-to-sealring:
	PDK_ROOT=$(PDK_ROOT) PDK=$(PDK) librelane --manual-pdk --run-tag $(TAG)_to_sealring --to Klayout.Sealring --overwrite config.yaml

.PHONY: librelane-from-sealring
librelane-from-sealring:
	PDK_ROOT=$(PDK_ROOT) PDK=$(PDK) librelane --manual-pdk --run-tag $(TAG)_from_sealring --overwrite --with-initial-state runs/$(TAG)/63-klayout-sealring/state_out.json --from GdsFill.Filler config.yaml

.PHONY: librelane-from-density
librelane-from-density:
	PDK_ROOT=$(PDK_ROOT) PDK=$(PDK) librelane --manual-pdk --run-tag $(TAG)_from_density --overwrite --with-initial-state runs/$(TAG)/59-klayout-sealring/state_out.json --from Klayout.Density config.yaml

.PHONY: view-results
view-results:
	PDK_ROOT=$(PDK_ROOT) PDK=$(PDK) librelane --manual-pdk --last-run --flow OpenInKlayout config.yaml
