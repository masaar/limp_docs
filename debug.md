[Back to Index](/README.md)

# Debug Mode
[LIMP CLI](/cli.md) has an option to start LIMPd with Debug Mode using `--debug` CLI `arg`, like:
```bash
python limpd.py --debug
```
Debug Mode makes the output of LIMPd verbose up to the point where every internal call is logged. This mode should never be used in production environments since it outputs huge amount of data in seconds. This mode is meant to be used on development and staging environments.

## Debug Mode and Test Workflow
When running LIMPd with _Test Workflow_, _Debug Mode_ is enabled automatically. This assures that developers have access to details when tests failed.