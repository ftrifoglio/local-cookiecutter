SHELL = /bin/bash
VENV_DIR = .venv
PYTHON_VERSION = {{ cookiecutter.python_version }}
# COLOURS
COLOUR_GREEN=\033[0;32m
COLOUR_RED=\033[0;31m
COLOUR_BLUE=\033[0;34m
COLOUR_END=\033[0m

.DEFAULT_GOAL = help

help:  ## Display this help
	@awk 'BEGIN {FS = ":.*##"; \
	printf "\nUsage: make\n\nTargets:\n"} \
	/^[a-zA-Z_-]+:.*?##/ \
	{ printf "$(COLOUR_BLUE)%-15s$(COLOUR_END) %s\n", $$1, $$2 }' \
	$(MAKEFILE_LIST)

venv:  ## Create environment
	@pyenv local $(PYTHON_VERSION)
	@poetry install
	@poetry add {{ cookiecutter.main_packages }}
	@poetry add {{ cookiecutter.dev_packages }} -D

.PHONY = clean

clean: ## Clean up environment
	@rm -rf $(VENV_DIR)
	@rm -f .python-version
	@find . | grep __pycache__ | xargs rm -rf
	@find . | grep .ipynb_checkpoints | xargs rm -rf
