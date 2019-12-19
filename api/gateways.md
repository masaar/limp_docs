[Back to API Reference Index](./README.md)

# Gateways
Gateways are methods available in LIMP eco-system for use by [modules](./module.md) as well as [jobs](./jobs.md). The best example of a gateway is access to external communication and messaging service. Starting API v5.8, [Gateways Workflow](../workflows/gateways-workflow.md) was introduced to allow developers to extend the available gateways.

## `Gateway`
`Gateway` controller is available for importing across LIMP eco-system. The controller is the accessor for gateways, whether built-in or third-party.

### Using `Gateway`
`Gateway` controller can be accessed by importing it, like:
```python
from gateway import Gateway
```

### `send` Method
`Gateway` controller has only one method which can be accessed [statically](https://docs.python.org/3/library/functions.html?highlight=static#staticmethod). `send` method requires one argument, `gateway`, which is a `str` type referring to the gateway to be used. Following the `gateway` argument, `send` method accepts any number of keyword-arguments to be passed to the gateway method.

#### Errors in `send`
`send` method doesn't check for the validity of of the gateway name, nor keyword arguments. If the app makes a call to non-existence gateway it would results in raising `KeyError Exception`. The same applies to keyword-arguments, if any of the arguments are missing from the gateway call, the error would be the exception raised by the gateway method.


## `email`
The only built-in gateway is `email` gateway. 