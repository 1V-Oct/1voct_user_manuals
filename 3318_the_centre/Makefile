# Makefile for building the multi-language manual

# Define the LaTeX compiler
LATEX_COMPILER ?= latexmk

# Define the base name for the TeX file
TEX_BASE = main

# Define the output directory
OUT_DIR ?= out

FILE_PREFIX = 3318_the_centre_

# Automatically find all language directories (e.g., en, pl, de) inside 'pages'
LANG_CODES := $(patsubst pages/%/,%,$(wildcard pages/*/))

# Find all .tex files in the shared directory to use as dependencies
SHARED_TEX_FILES := $(wildcard ../shared/*.tex)

# Define all possible PDF targets
ALL_PDFS := $(foreach lang,$(LANG_CODES),$(OUT_DIR)/$(FILE_PREFIX)$(lang).pdf)

# Targets
# If LANG is not specified on the command line, or if it's an invalid language
# (e.g., from the shell environment), build all available languages.
# Otherwise, build only the specified (and valid) language.
ifneq ($(filter $(LANG),$(LANG_CODES)),)
# LANG is set and is a valid language
all: $(OUT_DIR)/$(FILE_PREFIX)$(LANG).pdf
else
# LANG is not set, or is not a valid language code. Build all.
all: $(ALL_PDFS)
endif

pdf: all


# Generic rule to build a PDF for a given language
.SECONDEXPANSION:
$(OUT_DIR)/$(FILE_PREFIX)%.pdf: $(TEX_BASE).tex $(SHARED_TEX_FILES) $$(wildcard pages/$$*/*.tex) $$(wildcard pages/$$*/**/*.tex)
	$(LATEX_COMPILER) -xelatex -synctex=1 -jobname=$(FILE_PREFIX)$* -pretex="\def\LANG{$*}" -usepretex -output-directory=$(OUT_DIR) $(TEX_BASE).tex
# 	latexmk -xelatex -synctex=1 -interaction=nonstopmode -file-line-error --shell-escape -jobname="users-manual" -pretex="\def\LANG{$*}" -output-directory=out -usepretex manual

clean:
	rm -rf $(OUT_DIR)

.PHONY: all pdf clean