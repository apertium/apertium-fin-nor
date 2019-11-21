##############################################################################
## Makefile for Finnish--Norwegian
###############################################################################

VERSION=0.1.0
LANG1=fin
LANG2=nor
LANG2n=nno
LANG2b=nob
PREFIX1=$(LANG1)-$(LANG2)
PREFIX1b=$(LANG1)-$(LANG2b)
PREFIX1n=$(LANG1)-$(LANG2n)
PREFIX2=$(LANG2)-$(LANG1)
PREFIX2b=$(LANG2b)-$(LANG1)
PREFIX2n=$(LANG2n)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1b).autobil.bin \
	$(PREFIX1b).autogen.bin \
	$(PREFIX1b).autolex.bin \
	$(PREFIX1b).automorf.hfst \
	$(PREFIX1b).t1x.bin \
	$(PREFIX1b).t2x.bin \
	$(PREFIX1b).t3x.bin \
	$(PREFIX1n).autobil.bin	\
	$(PREFIX1n).autolex.bin	\
	$(PREFIX1n).autogen.bin	\
	$(PREFIX1n).t1x.bin	\
	$(PREFIX1n).t2x.bin	\
	$(PREFIX1n).t3x.bin	\
	$(PREFIX2n).automorf.bin	\
	$(PREFIX2b).automorf.bin	\
	$(PREFIX2b).prob		\
	$(PREFIX2n).prob		\
	$(PREFIX2n).rlx.bin	\
	$(PREFIX2b).rlx.bin	\
	$(PREFIX2).autobil.bin	\
	$(PREFIX2n).autolex.bin	\
	$(PREFIX2b).autolex.bin	\
	$(PREFIX2).autogen.hfst	\
	$(PREFIX2).t1x.bin	\
	$(PREFIX2).t2x.bin	\
	$(PREFIX2).t3x.bin

# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# Finnish analysis:
# -------------------

$(PREFIX1).automorf.hfst: $(AP_SRC1)/$(LANG1).automorf.hfst
	cp $< $@

$(PREFIX1b).automorf.hfst: $(AP_SRC1)/$(LANG1).automorf.hfst
	cp $< $@

$(PREFIX1n).automorf.hfst: $(AP_SRC1)/$(LANG1).automorf.hfst
	cp $< $@

# -------------------
# Finnish generation:
# ---------------------

$(PREFIX2).autogen.hfst: $(AP_SRC1)/$(LANG1).autogen.hfst
	cp $< $@

$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

# -------------------
# Norwegian analysis:
# -------------------

.deps/$(LANG2b).automorf.bin: $(AP_SRC2b)/$(LANG2b).automorf.bin .deps/.d
	cp $< $@

$(PREFIX2b).automorf.bin: .deps/$(LANG2b).automorf.bin $(PREFIX2).autobil.bin
	lt-trim $^ $@

.deps/$(LANG2n).automorf.bin: $(AP_SRC2n)/$(LANG2n).automorf.bin .deps/.d
	cp $< $@

$(PREFIX2n).automorf.bin: .deps/$(LANG2n).automorf.bin $(PREFIX2).autobil.bin
	lt-trim $^ $@

# -------------------
# Norwegian generation:
# ---------------------


$(PREFIX1b).autogen.bin: $(AP_SRC2b)/$(LANG2b).autogen.bin
	cp $< $@

$(PREFIX1n).autogen.bin: $(AP_SRC2n)/$(LANG2n).autogen.bin
	cp $< $@

###############################################################################
## Tagger models
###############################################################################

$(PREFIX2b).prob: $(AP_SRC2b)/$(LANG2b).prob
	cp $< $@

$(PREFIX2n).prob: $(AP_SRC2n)/$(LANG2n).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

$(PREFIX2b).rlx.bin: $(AP_SRC2b)/apertium-$(LANG2b).$(LANG2b).rlx
	cg-comp $< $@

$(PREFIX2n).rlx.bin: $(AP_SRC2n)/apertium-$(LANG2n).$(LANG2n).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

$(PREFIX1b).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp --var-right=nob lr $< $@

$(PREFIX1n).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp --var-right=nno lr $< $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

$(PREFIX1b).autolex.bin: $(BASENAME).$(PREFIX1b).lrx
	lrx-comp $< $@

$(PREFIX1n).autolex.bin: $(BASENAME).$(PREFIX1n).lrx
	lrx-comp $< $@

$(PREFIX2b).autolex.bin: $(BASENAME).$(PREFIX2b).lrx
	lrx-comp $< $@

$(PREFIX2n).autolex.bin: $(BASENAME).$(PREFIX2n).lrx
	lrx-comp $< $@


###############################################################################
## Structural transfer rules
###############################################################################


$(PREFIX1b).t1x.bin: $(BASENAME).$(PREFIX1b).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1b).t2x.bin: $(BASENAME).$(PREFIX1b).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1b).t3x.bin: $(BASENAME).$(PREFIX1b).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1n).t1x.bin: $(BASENAME).$(PREFIX1n).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1n).t2x.bin: $(BASENAME).$(PREFIX1n).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1n).t3x.bin: $(BASENAME).$(PREFIX1n).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1b).t1x	\
		$(BASENAME).$(PREFIX1b).t2x	\
		$(BASENAME).$(PREFIX1b).t3x	\
		$(BASENAME).$(PREFIX1n).t1x	\
		$(BASENAME).$(PREFIX1n).t2x	\
		$(BASENAME).$(PREFIX1n).t3x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2x	\
		$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_fin_nordir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_fin_nor_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1b).t1x			\
	$(BASENAME).$(PREFIX1b).t2x			\
	$(BASENAME).$(PREFIX1b).t3x			\
	$(BASENAME).$(PREFIX1n).t1x			\
	$(BASENAME).$(PREFIX1n).t2x			\
	$(BASENAME).$(PREFIX1n).t3x			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2x			\
	$(BASENAME).$(PREFIX2).t3x


# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	echo "talo" | apertium -d . fin-nob | tee .test-mt
	@echo "hus" > .test-ref
	@diff .test-ref .test-mt
	echo "hus" | apertium -d . nob-fin | tee .test-mt
	@echo "talo" > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt

