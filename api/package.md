[Back to API Reference Index](./README.md)

# Package
LIMP package is Python package that can be located in `modules` folder in LIMP root. The package-design structure in LIMP allows a developer to pack few modules under packages for reuse in different occasions. A LIMP package has three elements:
1. [Config](#package-config): Every package in LIMP has to define a `config` method that returns LIMP [`Config`](/api/config.md) matching dict.
2. Dependencies: LIMP package can define extra `requirements.txt` file including all the package dependencies which then be installed by [LIMPd CLI Interface](/cli.md).
3. Modules: Python modules that follow LIMP [modules](/api/module.md) guideline. These modules are where all the [methods](/api/method.py) are located and the logic happens.

## Package Config
LIMP package, which happens to be also a Python package should have `__init__` file. `__init__` file should have or import function with name `config`. Function `config` should return only Python `dict`, which keys are [`Config Attrs`](/api/config.md#config-attrs) and values are accepted values to the respective `Config Attr`.

If a package doesn't require any config, then function `config` should still exist and return empty Python `dict`.

Developers can always make use of [`envs` Config Attr](/api/config.md#envs) by passing values again in nested `envs` Config Attr `dict`.

## Package Dependencies
LIMP strict structure doesn't steal the freedom of using other Python libs. In addition to this, LIMP allows developers to define custom `requirements.txt` files in their package to flag what libs are required by every package. These `requirements.txt` files in every LIMP package can be easily installed using [LIMPd CLI `install-deps`](/cli.md) utility, as part of [Install Dependencies Workflow](/workflows/install-deps-workflow.md).

## Package Tests
LIMP [Test Workflow](/workflows/test-workflow.md) allows developers to define API-level tests per package which would allow developers to write unit tests as well as integration tests. Tests for package can be written as described in [Tests](/api/tests.md).

## Package Localisation
One of the advertised features of LIMP is being "Multi-language and Localisation-ready". This feature works on package-level to allow developers to make full use of such an aspect of LIMP. Package l10n dictionaries can be written as described in [l10n](/api/l10n.md)

## Package Modules
LIMP modules have their own reference that can be found [here](/api/module.md).