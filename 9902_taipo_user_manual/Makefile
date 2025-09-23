# Makefile for building the multi-language manual

# Define the LaTeX compiler
LATEX_COMPILER ?= xelatex

# Define the base name for the TeX file
TEX_BASE = main

# Define the output directory
OUT_DIR ?= out

# Automatically find all language directories (e.g., en, pl, de) inside 'pages'
LANGS := $(wildcard pages/*/)
LANG_CODES := $(patsubst pages/%/,%,$(LANGS))

# Generate PDF targets for each language
PDFS := $(foreach lang,$(LANG_CODES),$(OUT_DIR)/9902_taipo_user_manual_$(lang).pdf)

# Targets
all: pdf

pdf: $(PDFS)

# Generic rule to build a PDF for a given language
$(OUT_DIR)/9902_taipo_user_manual_%.pdf: $(TEX_BASE).tex preamble.tex titlepage.tex pages/%/content.tex
	mkdir -p $(OUT_DIR)
	$(LATEX_COMPILER) -jobname=9902_taipo_user_manual_$* -output-directory=$(OUT_DIR) "\def\LANG{$*}\input{$(TEX_BASE).tex}"
	# Run twice for table of contents and references
	$(LATEX_COMPILER) -jobname=9902_taipo_user_manual_$* -output-directory=$(OUT_DIR) "\def\LANG{$*}\input{$(TEX_BASE).tex}"

clean:
	rm -rf $(OUT_DIR)

.PHONY: all pdf clean