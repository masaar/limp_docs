[Back to API Reference Index](./README.md)

# Package
LIMP package is Python package that can be located in `modules` folder in LIMP root. The package-design structure in LIMP allows a developer to pack few modules under packages for reuse in different occasions. A LIMP package has three elements:
1. [Config](#package-config): Every package in LIMP has to define a `config` method that returns LIMP [`Config`](/api/config.md) matching dict.
2. Dependencies: LIMP package can define extra `requirements.txt` file including all the package dependencies which then be installed by [LIMPd CLI Tool](/api/cli-tool.md).
3. Modules: Python modules that follow LIMP [modules](/api/module.md) guideline. These modules are where all the [methods](/api/method.py) are located and the logic happens.

## Package Config
LIMP package, wich happens to be also a Python package should have `__init__` file. `__init__` file should have or import function with name `config`. Function `config` should return only Python `dict`, which keys are [`Config Attrs`](/api/config.md#config-attrs) and values are accepted values to the respective `Config Attr`.

If your package doesn't require any config, then function `config` should still exist and return empty Python `dict`.

Developers can always make use of [`envs` Config Attr](/api/config.md#envs) by passing values again in nested `envs` Config Attr `dict`.

## Package Dependencies
LIMP strict structure doesn't steal the freedom of using other Python libs. In addition to this, LIMP allows developers to define custom `requirements.txt` files in their package to flag what libs are required by every package. These `requirements.txt` files in every LIMP package can be easily installed using [LIMPd CLI Tool `install-deps`](/api/cli-tool.md#install-deps).

## Package Modules
LIMP modules have their own reference that can be found [here](/api/module.md).