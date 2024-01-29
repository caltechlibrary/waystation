# Summary: Makefile for building docs using Sphinx and MyST
#
# Copyright 2024 California Institute of Technology.
# License: Modified BSD 3-clause – see file "LICENSE" in the project website.
# Website: https://github.com/caltechlibrary/waystation

# Before we go any further, test if certain programs are available.
# The following is based on the approach posted by Jonathan Ben-Avraham to
# Stack Overflow in 2014 at https://stackoverflow.com/a/25668869

PROGRAMS_NEEDED = sphinx-build
TEST := $(foreach p,$(PROGRAMS_NEEDED),\
	  $(if $(shell which $(p)),_,$(error Cannot find program "$(p)")))


# Gather values that we need ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

# You can set the following variables from the command line, and also from
# the environment for the first two.

SPHINXOPTS  ?=
SPHINXBUILD ?= sphinx-build
SPHINXAUTO  = sphinx-autobuild
SOURCEDIR   = .
BUILDDIR    = _build

# Actions ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

# Put it first so that "make" without argument is like "make help".
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

auto autobuild live livehtml:
	@$(SPHINXAUTO) "$(SOURCEDIR)" "$(BUILDDIR)"/html $(SPHINXOPTS) $(O)

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)


# Cleanup and miscellaneous directives ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.PHONY: help auto autobuild livehtml Makefile
