# Sphinx Needs Test

A test to show matplotlib-less sphinx-needs

Requires Python 3.10


## Usage

Install the dependencies, and prove that no matplotlib or numpy is present.

    make install export-requirements 
    # Alias for
    # poetry run pip freeze > requirements.txt
    grep -i "matplotlib" requirements.txt  # 0 rows returned
    grep -i numpy requirements.txt  # 0 rows returned
    poetry show matplotlib   # No such dependency
    poetry show numpy  # No such dependency
    make docs docs-serve  # Docs built using sphinx-needs (Architecture page)


Compare with the dependency list of sphinx-needs:

    poetry show sphinx-needs

Which returns:
    name         : sphinx-needs                                                              
    version      : 1.0.2                                                                     
    description  : Sphinx needs extension for managing needs/requirements and specifications 

    dependencies
    - docutils >=0.15
    - esbonio >=0.11.3
    - jsonschema 3.2.0
    - pygls *
    - requests ^2.25.1
    - requests-file ^1.5.1
    - sphinx >=5.0
    - sphinx-data-viewer ^0.1.1
    
Note no matplotlib or numpy!

In details via `poetry show -t sphinx-needs`

    sphinx-needs 1.0.2 Sphinx needs extension for managing needs/requirements and specifications
    ├── docutils >=0.15
    ├── esbonio >=0.11.3
    │   ├── appdirs * 
    │   ├── pygls >=0.11.0 
    │   │   ├── pydantic >=1.9.1,<1.10 
    │   │   │   └── typing-extensions >=3.7.4.3 
    │   │   └── typeguard >=2.10.0,<3 
    │   ├── pyspellchecker * 
    │   ├── sphinx * 
    │   │   ├── alabaster >=0.7,<0.8 
    │   │   ├── babel >=2.9 
    │   │   │   └── pytz >=2015.7 
    │   │   ├── colorama >=0.4.5 
    │   │   ├── docutils >=0.14,<0.20 
    │   │   ├── imagesize >=1.3 
    │   │   ├── jinja2 >=3.0 
    │   │   │   └── markupsafe >=2.0 
    │   │   ├── packaging >=21.0 
    │   │   │   └── pyparsing >=2.0.2,<3.0.5 || >3.0.5 
    │   │   ├── pygments >=2.12 
    │   │   ├── requests >=2.5.0 
    │   │   │   ├── certifi >=2017.4.17 
    │   │   │   ├── charset-normalizer >=2,<3 
    │   │   │   ├── idna >=2.5,<4 
    │   │   │   └── urllib3 >=1.21.1,<1.27 
    │   │   ├── snowballstemmer >=2.0 
    │   │   ├── sphinxcontrib-applehelp * 
    │   │   ├── sphinxcontrib-devhelp * 
    │   │   ├── sphinxcontrib-htmlhelp >=2.0.0 
    │   │   ├── sphinxcontrib-jsmath * 
    │   │   ├── sphinxcontrib-qthelp * 
    │   │   └── sphinxcontrib-serializinghtml >=1.1.5 
    │   └── typing-extensions * (circular dependency aborted here)
    ├── jsonschema 3.2.0
    │   ├── attrs >=17.4.0 
    │   ├── pyrsistent >=0.14.0 
    │   ├── setuptools * 
    │   └── six >=1.11.0 
    ├── pygls *
    │   ├── pydantic >=1.9.1,<1.10 
    │   │   └── typing-extensions >=3.7.4.3 
    │   └── typeguard >=2.10.0,<3 
    ├── requests ^2.25.1
    │   ├── certifi >=2017.4.17 
    │   ├── charset-normalizer >=2,<3 
    │   ├── idna >=2.5,<4 
    │   └── urllib3 >=1.21.1,<1.27 
    ├── requests-file ^1.5.1
    │   ├── requests >=1.0.0 
    │   │   ├── certifi >=2017.4.17 
    │   │   ├── charset-normalizer >=2,<3 
    │   │   ├── idna >=2.5,<4 
    │   │   └── urllib3 >=1.21.1,<1.27 
    │   └── six * 
    ├── sphinx >=5.0
    │   ├── alabaster >=0.7,<0.8 
    │   ├── babel >=2.9 
    │   │   └── pytz >=2015.7 
    │   ├── colorama >=0.4.5 
    │   ├── docutils >=0.14,<0.20 
    │   ├── imagesize >=1.3 
    │   ├── jinja2 >=3.0 
    │   │   └── markupsafe >=2.0 
    │   ├── packaging >=21.0 
    │   │   └── pyparsing >=2.0.2,<3.0.5 || >3.0.5 
    │   ├── pygments >=2.12 
    │   ├── requests >=2.5.0 
    │   │   ├── certifi >=2017.4.17 
    │   │   ├── charset-normalizer >=2,<3 
    │   │   ├── idna >=2.5,<4 
    │   │   └── urllib3 >=1.21.1,<1.27 
    │   ├── snowballstemmer >=2.0 
    │   ├── sphinxcontrib-applehelp * 
    │   ├── sphinxcontrib-devhelp * 
    │   ├── sphinxcontrib-htmlhelp >=2.0.0 
    │   ├── sphinxcontrib-jsmath * 
    │   ├── sphinxcontrib-qthelp * 
    │   └── sphinxcontrib-serializinghtml >=1.1.5 
    └── sphinx-data-viewer ^0.1.1

### Run the command

Install the module first:

    make install
    # or
	poetry install

Then inside the virtual environment, launch the command:

    # Run single command inside virtualenv
    poetry run sphinx-needs-test

    # or
    # Load the virtualenv first
    poetry shell
    # Then launch the command, staying in virtualenv
    sphinx-needs-test

## Development

### Python setup

This repository uses Python3.10, using
[Poetry](https://python-poetry.org) as package manager to define a
Python package inside `src/sphinx_needs_test/`.

`poetry` will create virtual environments if needed, fetch
dependencies, and install them for development.


For ease of development, a `Makefile` is provided, use it like this:

	make  # equivalent to "make all" = install lint docs test build
	# run only specific tasks:
	make install
	make lint
	make test
	# Combine tasks:
	make install test

Once installed, the module's code can now be reached through running
Python in Poetry:

	$ poetry run python
	>>> import sphinx_needs_test
	>>> print(sphinx_needs_test.version)
	"0.1.0"

This codebase uses [pre-commit](https://pre-commit.com) to run linting
tools like `flake8`. Use `pre-commit install` to install git
pre-commit hooks to force running these checks before any code can be
committed, use `make lint` to run these manually. Testing is provided
by `pytest` separately in `make test`.

### Documentation

Documentation is generated via [Sphinx](https://www.sphinx-doc.org/en/master/),
using the cool [myst_parser](https://myst-parser.readthedocs.io/en/latest/)
plugin to support Markdown files like this one.

Other Sphinx plugins provide extra documentation features, like the recent
[AutoAPI](https://sphinx-autoapi.readthedocs.io/en/latest/index.html) to
generate API reference without headaches.

To build the documentation, run

    # Requires the project dependencies provided by "make install"
    make docs
	# Generates docs/build/html/

To browse the website version of the documentation you just built, run:

    make docs-serve

And remember that `make` supports multiple targets, so you can generate the
documentation and serve it:

    make docs docs-serve


### Templated

This repo is templated, using commit hash: `f2bee7034b85f6f71cdcfb4b7f9350ea7de8af4b`
