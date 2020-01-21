[Back to API Reference Index](./README.md)

# Config
Config in LIMP eco-system are the loaded configurations of the current LIMPd instance according to various [LIMPd CLI](/api/cli.md) run parameters.

## Config Attrs
Single config item is referred to as `Config Attr`. Config Attrs are populated from the loaded [packages](/api/package.md) against the default values of the Config Attrs.

### `api_level`
LIMP API-level as string which the app was developed to be used for. If set, this would trigger a version check at the the launch time. The version should be the `version.major` number dropping the minor number. Setting this value is highly recommended and ignoring it would raise a runtime warning. default `None`.

### `packages_versions`
At package-level this is a string representation of LIMP package version, which is present for debugging and app management reasons. On Config controller side, this would be populated as `dict` with package names be the keys and corresponding packages versions are the values.

### `envs`
An environment projection object. This can be used to create `Config Environment` per need. For instance, all the package Config Attrs can be reused in every Config Environment defined in `envs`. The most essential use-case here is using two set of `data_*` Config Attrs set among two `envs`; `dev` and `prod`:
```python
{
	'dev':{
		'data_server':'mongodb://localhost'
	},
	'prod':{
		'data_server':'mongodb://remotehost'
	}
}
```
Such feature allows the developers to develop in their development `env` and then deploy the app to their `prod` host, and it would still work without a single change to any of the package or app config. Default `{}`.

### `emulate_test`
Flag to dynamically set `test` Config Attr to `True` after app is loaded. This allow LIMP apps to mimic test conditions in order to skip production-level calls and functions without the need to change the code. Learn about this strategy in [`LIMP Tests`](/tests.md#emulate_test). Default `False`.

### `realm`
Flag to set the app to run in Realm mode. This is an advanced use-case of LIMP that has very specific scenario. Learn more about this mode in the [full reference of Realm mode](/api/realm.md). Default `False`.

### `vars`
General purpose storage. This can be used to store any data to use across LIMP apps. Default `{}`.

### `client_apps`
Python `dict` to be used in both [Connection Verification Workflow](/workflows/conn-verification-workflow.md) and [Analytics Workflow](/workflows/analytics-workflow.md). Keys of `client_apps` are the `app_id`s that will be used by client apps connecting to LIMP app using any of the SDKs available. Values are Python `dict` with the attributes set based on app type like following:
```python
{
	'web_app_id': {
		'name': 'my_web_app', # Human readable name for use in Analytics Workflow
		'type': 'web', # Type of the client app to determine Connection Verification Workflow Sequence
		'hosts': ['https://my-web-app-address', 'https://my-web-app-alt-address'], # List of hosts this app will be allowed to connect from.
	},
	'mobile_app_id': {
		'name': 'my_mobile_app',
		'type': 'android', # Can be set to 'ios' as well.
		'app_id_hash': 'some_hash', # Hash generated from hashing ['mobile_app_id', 'my_mobile_app'] with mobile app signature.
	},
}
```
Default `[]`.

### `analytics_events`
Python `dict` with key, value pairs of the status of LIMP built-in analytics events as part of [Analytics Workflow](/workflows/analytics-workflow.md). By default, all events are set to `True`, if any of the events are not wanted it can be passed as part of this Config Attr with value set to `False`. Default:
```python
{
	'app_conn_verified': True,
	'session_conn_auth': True,
	'session_user_auth': True,
	'session_conn_reauth': True,
	'session_user_reauth': True,
	'session_conn_deauth': True,
	'session_user_deauth': True,
}
```

### `conn_timeout`
Value of [Connection Timeout Workflow](/workflows/conn-timeout-workflow.md). Default `120`.

### `quota_anon_min`
Value of calls quota for non-authenticated sessions of [Calls Quota Workflow](/workflows/calls-quota-workflow.md). Default `40`.

### `quota_auth_min`
Value of calls quota for authenticated sessions of [Calls Quota Workflow](/workflows/calls-quota-workflow.md). Default `100`.

### `quota_ip_min`
Value of calls quota per IP of [Calls Quota Workflow](/workflows/calls-quota-workflow.md). Default `500`.

### `data_server`
Data server to connect to. Usually it's string, however, if you are connecting to MongoDB ReplicaSet with multiple servers you can specify this Config Attr as a list of strings each representing a different server. LIMP would automatically detect this and attempt to connect to the servers one by one until one is connected successfully. Default `'mongodb://localhost'`.

### `data_name`
Database name to connect to. Default `'limp_data'`.

### `data_ssl`
Boolean flag on whether to use secure `SSL` connection or not. Default `False`,

### `data_ca_name`
Name of the CA certificate to use while connecting to `data_server`. The certificate would be dynamically created at runtime in `certs` folder in your app root. This folder is not tracked by LIMP Git repo, which is the reason you don't see it in your cloned repo. Default `False`.

### `data_ca`
CA certificate usage flag and body. If it's set, the `data` connection with `data_server` would be constructed with this CA file, as `data_ca_name`. For this, if `data_ca` is having any truth-matching value, `data_ca_name` should also be present and valid. In Python, you should paste your certificate as-is including the line breaks. For that you need to make sure you are using the multi-line string. Make sure you don't add any wrong indentations when pasting the certificate body. This Config Attr was added to support IBM Cloud Databases for MongoDB which requires a CA certificate for connection. Default `False`.

### `data_disk_use`
Value on whether [`allowDiskUse`](https://docs.mongodb.com/manual/reference/command/aggregate/#aggregate-data-using-external-sort) of `MongoDB` should be passed along `Data` calls or not. Default `False`.

### `data_azure_mongo`
Microsoft's Azure-specific MongoDB-in-sharded mode (or, [database throughput](https://docs.microsoft.com/en-us/azure/cosmos-db/how-to-provision-database-throughput)). The problem with databases created under this mode in Azure is the developer need to execute MongoDB command `shardCollection` to create the collection with assignment of `hashed_key` at the time of creation. For that, we introduced this Config Attr that you can set to `True` to do this on behalf of the developers for all the collections of all the modules of the current loaded app. Default `False`.

### `email_auth`
Python `dict` with `server`, `username` and `password` of the default email account to send notifications from. Default `{}`.

### `locales`
Python list of locales used by the package. The form of the locale used in LIMP is `lang_COUNTRY`. Default `['ar_AE', 'en_AE']`.

### `locale`
Default locale of the app. It should be one of the values passed in `locales`. Default `ar_AE`.

### `admin_doc`
`ADMIN` doc. Fully qualified user doc to be used for creating `ADMIN` user. Default `{}`.

### `admin_password`
`ADMIN` password. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning. Default `'__ADMIN'`.

### `anon_token`
`ANON` user session token. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning. Default `'__ANON_TOKEN_f00000000000000000000012'`.

### `anon_privileges`
`ANON` user privileges. These are the privileges that any anonymous user of the app would have. Learn more about privileges from the reference of [LIMP privileges](/api/privilege.md). Default `{}`.

### `user_attrs`
Python `dict` representing additional attrs to update [`User` LIMP module](../core/user.md) with. This `dict` should at least have one attr that is used as [`auth_attr`](../core/user.md#auth_attrs). Default `{}`.

### `user_auth_attrs`
Python `list` of `User` LIMP module to use as [`auth_attrs`](../core/user.md#auth_attrs). At least one `auth_attr` should be present. Default `[]`.

### `user_attrs_defaults`
Python `dict` representing value of [`User` LIMP module](../core/user.md#auth_attrs) `defaults` attr. Default `{}`.

### `user_settings`
...

### `groups`
App-specific users groups to create. This is a list of docs, each representing a group. Specifying `_id` of the group docs is a must. Default `[]`.

### `default_privileges`
`DEFAULT` group privileges. These are the privileges that all your app users would have. Default `{}`.

### `data_indexes`
List of app-specific data indexes to create for data collections. This is an array of all the indexes you want to create for your app to function. For instance, to create a MongoDB `$text` index on collection `staff` you can set `data_indexes` to:
```python
[
	{
		'collection': 'staff',
		'index': [( '$**', 'text' )]
	}
]
```
Notice that the name you are passing is the `collection` name and not the module name. Also, the `index` attribute is the native `index` format you pass to your MongoDB driver. Default `[]`.

### `docs`
List of app-specific docs to create for the app functionalities. Every list item is a Python `dict` with two attributes; `module` and `doc`. The docs would be created using LIMP [base create method](/api/method.md#create). For instance, to create `setting` doc in your app you should set `docs` to:
```python
[
	{
		'module':'setting',
		'doc':{
			'_id':ObjectId('a00000000000000000000091'),
			'user':ObjectId('f00000000000000000000010'),
			'var':'company_name',
			'val':{
				'ar_AE':'أكمي',
				'en_AE':'ACME'
			},
			'type':'global'
		}
	}
]
```
Optionally, you can add `skip_args` with value set to `True` in the `dict` to force appending of `__ARGS__` to skipped event. This is helpful when you need to force creating a doc without validating it. This follows [`skip_events` sequence](/api/call.md#skip_events).

### `jobs`
List of app-specific recurring jobs using [`Jobs Workflow`](/api/jobs.md). Default `[]`.

### `gateways`
App-specific gateways dictionary. This Python dict is used by [`Gateways Workflow`](/api/gateways.md) with the key representing the gateway name, and the key being Python `callable` the serves as the gateway. Default `{}`.

### `types`
App-specific [Attrs Types](/api/attrs-types.md). This is a Python `dict` with pair of key representing the type name and value being a Python `callable` that has the following signature:
```python
(attr_name: str, attr_type: str, attr_val: Any)
```
The `callable` should return `attr_val` as-is or converted if required, or raise one of the [Attrs Types Exceptions](/api/attrs-types.md#attrs-types-exceptions) upon any failure.


> Some of Config Attrs are available but not supposed to be set by package Config, but still available to LIMP modules to access and read their values, which are:
### `debug`
The flag of whether debug options are active or not. It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `env`
The name of the current `env`. It's not supposed to be set by a package, rather by the CLI. Default `None`.

### `_sys_conn`
...

### `_sys_env`
...

### `_sys_docs`
Current instance dictionary of `System Docs`. This is LIMP-generated dict that prevents LIMP apps from wrongly deleting docs that are essential for its runtime. This Config Attr is mainly used by [`Call Delete Strategies`](/api/call.md#delete-strategies). It's not supposed to be set by a package. Default `{}`.

### `_realms`
Current instance dictionary of [`Realms`](/api/realm.md). This is LIMP-generated dict that represents list of current realms in order to manage access to LIMP app according to available realms. It's not supposed to be set by a package. Default `{}`.

### `_jobs_session`
...

### `_jobs_base`
...

### `_limp_version`
Current LIMP version. This is populated from `version.txt` in the top-level dir of LIMP. This is used as placeholder to store the value for later use by `Config` object. It's not supposed to be set by a package. Default `None`.

### `_limp_location`
...

### `test`
The flag whether [`Test Workflow`](/api/test.md) is active or not. If it's active it should be string representing the test name. It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `test_skip_flush`
The flag whether [`Test Workflow`](/api/test.md) should skip flushing and dropping the previous test collections or not It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `test_force`
The flag whether [`Test Workflow`](/api/test.md) should break or force testing all steps after first failure. It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `test_env`
The flag whether [`Test Workflow`](/api/test.md) should run the test on the active `env` collections rather than using test collections. This is a destructive method that is explained in [`Test Workflow` API reference](/api/test.md). It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `test_breakpoint`
The flag whether to enable `Test Workflow` [`Debugger Break`](/api/test.md#debugger-break) feature. It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `test_collections`
The flag whether to start LIMP app with test collections rather than active `env` collections. This is an alt test strategy explained in [`LIMP Tests`](/tests.md#test_collections). It's not supposed to be set by a package, rather by the CLI. Default `False`.

### `tests`
...

### `generate_ref`
...

### `_api_ref`
...

### `l10n`
...

### `modules`
...

## Environnement Variables for Data Config Attrs
In order to keep LIMP flexible to all use-cases, the ability to set `data_*` Config Attrs using environment variables was presented. This applies to:
* `data_server`
* `data_name`
* `data_ssl`
* `data_ca_name`
* `data_ca`

To use environment variables for any of the previously listed Config Attrs, set the value to environment variable name prefixed with `$__env.` like:
```python
'data_CONFIG_ATTR':'$__env.ENV_VAR_NAME'
```