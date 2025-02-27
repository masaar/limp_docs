[Back to Index](/README.md)

> This is a WIP. The actual tutorial was not designed yet. Once a design is set for a rich app that makes use of all the aspects of LIMP this tutorial would be updated with the same.

# Building an App with LIMP
Our `limp-sample-app` gives a good starting point. However, there's more than that.

The project consists of one package app. To understand the app structure you need to learn the following:

## Packages
A package is a folder with number of python files containing LIMP modules. The package has a distinguishing `__init__.py` file (which is also a requirement of Python packages) that sets the configurations of a package. An app in the LIMP ecosystem could be the results of multiple packages. That's one reason to allow LIMP structure to have more than a single package with the ability to manage which to include in the launching sequence using [LIMP CLI interface](/cli.md).

If your package uses any extra Python libs other than [dependencies](/dependencies.md) of LIMP, then you can add your `requirements.txt` file with those libs and it would be installed with LIMP dependencies when running [install dependencies](/quick-start#install-dependencies).

Learn more about packages in the [full API reference of packages](/api-package.md).

## Modules
A LIMP module is a single class in a Python file inside a LIMP package inheriting from LIMP's built-in `BaseModule` class. The `BaseModule` singletons all LIMP modules and provides them with access to the unified internal API for exchanging data.

A module is essentially a definition of a data-type with number of typed-[attrs](#attrs) that can be set as `optional_attrs` and/or auto-extended by documents from the same and/or another module using the `extns` instructions. A module as well defines all its `methods` that any client could call. By default the `CRUD` methods, `read`, `create`, `update`, `delete` are available for all of the modules by simply defining them. Additional methods can be defined either for use by the `HTTP/1 GET` interface or more often the `HTTP/2 Websocket` interface, using some additional instructions passed. A method can set the permissions checks required for an agent to pass before the agent being allowed to access the called method.

Learn more about modules in the [full API reference of modules](/api-module.md).

# Ancora Imparo
We love the `Hello, World!` gesture. But, in LIMP there's more than simply writing a simple app to start. There's always something to learn. There's `Ancora Imparo`--Our mascot!

Whether Michaelangelo said it or not, the famous `I'm still learning` quote is something the original author of LIMP believes in, and this belief was set in action in the development of LIMP. For this we would be building a `Ancora Imparo` app rather than a `Hello, World!` one.

What we will build in this lengthy tutorial is:
1. A utility package.
2. A package representing a Twitter clone app in conjunction with the utility package.
3. A package representing an Instagram clone app in conjunction with the utility package.

