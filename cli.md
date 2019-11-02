[Back to Index](/README.md)

# CLI Interface
LIMPd is your one-stop script in LIMP ecosystem. It allows you to [install dependencies](/dependencies.md), [test your packages](/test.md), and of course run your app with highly config runtime command line args. Full reference to usage of LIMP CLI interface:
```
usage: limpd.py [-h] [--version] [--install-deps] [--env ENV] [--debug] [--log] [--packages PACKAGES] [-p PORT]
                [--test TEST] [--test-flush] [--test-force] [--test-env] [--test-breakpoint] [--test-collections]

optional arguments:
  -h, --help            show this help message and exit
  --version             Show LIMP version and exit
  --install-deps        Install dependencies for LIMP and packages
  --env ENV             Choose specific env
  --debug               Enable debug mode
  --log                 Enable debug mode and log all debug messages to log file
  --packages PACKAGES   List of packages separated by commas to be loaded
  -p PORT, --port PORT  Set custom port [default 8081]
  --test TEST           Run specified test
  --test-flush          Flush previous test data collections
  --test-force          Force running all test steps even if one is failed
  --test-env            Run tests on selected env rather than sandbox env
  --test-breakpoint     Create debugger breakpoint upon failure of test.
  --test-collections    Enable Test Collections Mode.
```

## Using Environment Variables
Since one of the major use-cases of LIMP is to build a [`Docker` Image](/docker-image.md) for the app. Modifying some of the CLI values might not be that accessible on all platforms. For that, LIMPd has the ability to detect the following environnement variables:
* `PORT`: If environment variable `PORT` is detected and no `port` value was supplied to LIMPd, this environment variable value would be used as the port LIMP app is being served on.
* `ENV`: If environment variable `ENV` is detected and no `env` value was supplied to LIMPd, this environment variable value would be used as the `env` LIMP app is being set to.
* `DEBUG`: If environment variable `DEBUG`, regardless of its value, LIMP app would be starting with [`debug mode`](/debug.md).