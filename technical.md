[Back to Index](/README.md)

# Technical Sepcs
LIMP is built as future-proof framework, for that it always adapted up-to-date standards and methodologies while it's in development. This makes LIMP mostly requiring up-to-date environnement to work.

## Programming Language
LIMP is written with [Python](https://www.python.org/). As of the current version of LIMP it requires Python 3.7 or Python 3.8. Older versions of Python will not work and would require manual patching for essential elements of LIMP.

## Base Structure
Under the hood, LIMP is heavily based on Python [`asyncio`](https://docs.python.org/3/library/asyncio.html) lib for internal communication between elements of LIMP. LIMP also uses [`aiohttp`](https://aiohttp.readthedocs.io/en/stable/) to handle connections over `HTTP/2 Websocket`, and `HTTP/1 GET, POST` interfaces.

### LIMP Calls
Although LIMP depends mainly on `HTTP/2 Websocket`, however LIMP implements request-response calls over websocket. This allows developers to have more options when building their apps, while maintaining the advantages of websocket protocol, like preserving session info over the connection and faster messages transmission both ways.

## LIMP Modules
LIMP Modules are described in [Module API Reference](/api/module.md). In most of its parts, LIMP Modules are Python classes with specific attributes of Python dicts, lists and strings. The classes are then scaffolded using [`BaseModule`](/api/module#basemodule.md) on two steps with `__init__` and `__initialise` methods.

## LIMP Sandbox
LIMP has an accompanying [Sandbox](https://github.com/masaar/limp-sandbox) tool. Originally designed to test [LIMP SDK for Angular](https://github.com/masaar/ng-limp), the tool has proven to be much needed tool for debugging as well as assisting development of LIMP apps. LIMP Sandbox source can be cloned and built locally. LIMP Sandbox is also available on Github Pages for direct use over the following link: [https://masaar.github.io/limp-sandbox/dist/limp-sandbox](https://masaar.github.io/limp-sandbox/dist/limp-sandbox).