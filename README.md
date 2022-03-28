# python-lsp-black

[![PyPI](https://img.shields.io/pypi/v/python-lsp-black.svg)](https://pypi.org/project/python-lsp-black) [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Python](https://github.com/python-lsp/python-lsp-black/actions/workflows/python.yml/badge.svg)](https://github.com/python-lsp/python-lsp-black/actions/workflows/python.yml)

[Black](https://github.com/psf/black) plugin for the [Python LSP Server](https://github.com/python-lsp/python-lsp-server).

## Install

In the same `virtualenv` as `python-lsp-server`:

```shell
pip install python-lsp-black
```

# Usage

To avoid unexpected results you should make sure `yapf` and `autopep8` are not installed.

- `python-lsp-black` can either format an entire file or just the selected text.
- The code will only be formatted if it is syntactically valid Python.
- Text selections are treated as if they were a separate Python file.
  Unfortunately this means you can't format an indented block of code.
- `python-lsp-black` will use your project's
  [pyproject.toml](https://github.com/psf/black#pyprojecttoml) if it has one.
- `python-lsp-black` only officially supports the latest stable version of
  [black](https://github.com/psf/black). An effort is made to keep backwards-compatibility
  but older black versions will not be actively tested.
- The plugin can cache the black configuration that applies to each Python file, this
  improves performance of the plugin. When configuration caching is enabled any changes to
  black's configuration will need the LSP server to be restarted. Configuration caching
  can be disabled with the `cache_config` option, see *Configuration* below.

# Configuration

The plugin follows [python-lsp-server's
configuration](https://github.com/python-lsp/python-lsp-server/#configuration). These are
the valid configuration keys:

- `pylsp.plugins.black.enabled`: boolean to enable/disable the plugin.
- `pylsp.plugins.black.cache_config`: a boolean to enable black configuration caching (see
  *Usage*). `false` by default.
- `pylsp.plugins.black.line_length`: an integer that maps to [black's
  `max-line-length`](https://black.readthedocs.io/en/stable/the_black_code_style/current_style.html#line-length)
  setting. Defaults to 88 (same as black's default). This can also be set through black's
  configuration files, which should be preferred for multi-user projects.
- `pylsp.plugins.black.preview`: a boolean to enable or disable [black's `--preview`
  setting](https://black.readthedocs.io/en/stable/the_black_code_style/future_style.html#preview-style).

# Development

To install the project for development you need to specify the dev optional dependencies:

```shell
python -m venv .venv
. .venv/bin/activate
pip install -e .[dev]
```

This project uses [pre-commit](https://pre-commit.com/) hooks to control code quality,
install them to run automatically when creating a git commit, thus avoiding seeing errors
when you create a pull request:

```shell
pre-commit install
```

To run tests:

```shell
make test
```

To run linters:

```shell
make lint  # just a shortcut to pre-commit run -a
make <linter_name>  # black, flake8, isort, mypy
```

To upgrade the version of the pre-commit hooks:

```shell
pre-commit autoupdate
# check and git commit changes to .pre-commit-config.yaml
```
