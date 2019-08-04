# Config
Config in LIMP eco-system are the loaded configs of the current LIMPd instance according to various [LIMPd CLI Tool](/api/cli-tool.md) run paramaeters. Single config item is referred to as `Config Attr`. Config Attrs are populated from the loaded [packages](/api.package.md) against the default values of the Config Attrs.

## `version`
LIMP version as float which the app was developed to be used for. If set, this would trigger a version check at the the launch time. The version should be the `version.major` number dropping the minor number. Setting this value is highlt recommended and ignoring it would raise a runtime warning. default `None`.

## `envs`
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

## `tests`
The Test Workflow tests. These are the tests defined for the package. Learn more about Test Workflow and how to make use of the TDD-approach in LIMP in [Test Workflow reference](/api/test.md). Default `{}`.

## `data_server`
Data server to connect to. Usually it's string, however, if you are connecting to MongoDB ReplicaSet with multiple servers you can specify this Config Attr as a list of strings each representing a different server. LIMP would automatically detect this and attempt to connect to the servers one by one until one is connected successfully. Default `'mongodb://localhost'`.

## `data_name`
Database name to connect to. Default `'limp_data'`.

## `data_ssl`
Boolean flag on whether to use secure `SSL` connection or not. Default `False`,

## `data_ca_name`
Name of the CA certificate to use while connecting to `data_server`. The certificate would be dynamically created at runtime in `certs` folder in your app root. This folder is not tracked by LIMP Git repo, which is the reason you don't see it in your cloned repo. Default `False`.

## `data_ca`
CA certificate usage flag and body. If it's set, the `data` connection with `data_server` would be constructed with this CA file, as `data_ca_name`. For this, if `data_ca` is having any truth-matching value, `data_ca_name` should also be present and valid. In Python, you should paste your certificate as-is including the line breaks. For that you need to make sure you are using the multi-line string. Make sure you don't add any wrong indentations when pasting the certificate body. This Config Attr was added to support IBM Cloud Databases for MongoDB which requires a CA certificate for connection. Default `False`.

## `data_azure_mongo`
Microsoft's Azure-specific MongoDB-in-sharded mode (or, [database throughput](https://docs.microsoft.com/en-us/azure/cosmos-db/how-to-provision-database-throughput)). The problem with databases created under this mode in Azure is the developer need to execute MongoDB command `shardCollection` to create the collection with assignment of `hashed_key` at the time of creation. For that, we introduced this Config Attr that you can set to `True` to do this on behalf of the developers for all the collections of all the modules of the current loaded app. Default `False`.

## `sms_auth`
Python `dict` with Twilio `sid`, `token`, and `number` values to access their API. Default `{}`.

## `email_auth`
Python `dict` with `server`, `username` and `password` of the default email account to send notifications from. Default `{}`.

## `locales`
Python list of locales used by the package. The form of the locale used in LIMP is `lang_COUNTRY`. Default `['ar_AE', 'en_AE']`.

## `locale`
Default locale of the app. It should be one of the values passed in `locales`. Default `ar_AE`.

## `l10n`
App-specific locale dictionary. This is basically free form Python `dict` that can be used to store terms in different locales and then access them and use them from [LIMP methods](/api/method.md). Default `{}`.

## `admin_username`
`ADMIN` username. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning.  Default `__ADMIN`.

## `admin_email`
`ADMIN` email. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning. Default `ADMIN@LIMP.MASAAR.COM`.

## `admin_phone`
`ADMIN` phone. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning. Default `'+971500000000'`.

## `admin_password`
`ADMIN` password. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning. Default `'__ADMIN'`.

## `anon_token`
`ANON` user session token. Setting this value is a must to avoid security breaches and ignoring it would raise a runtime warning. Default `'__ANON_TOKEN_f00000000000000000000012'`.

## `anon_privileges`
`ANON` user privileges. These are the privileges that any anonymous user of the app would have. Learn more about privileges from the reference of [LIMP privileges](/api/privilege.md). Default `{}`.

## `groups`
App-specific users groups to create. This is a list of docs, each representing a group. Specifying `_id` of the group docs is a must. Default `[]`.

## `default_privileges`
`DEFAULT` group privileges. These are the privileges that all your app users would have. Default `{}`.

## `data_indexes`
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

## `docs`
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

## `realm`
Flag to set the app to run in Realm mode. This is an advanced use-case of LIMP that has very specific scenario. Learn more about this mode in the [full reference of Realm mode](/api/realm.md).

## `types`
App-specific [Attrs Types](/api/attrs-types.md). This is a Python `dict` with pair of key representing the type name and value being a Python `callable` that has the following signaure:
```python
(attr_name: str, attr_type: str, attr_val: Any)
```
The `callable` should return `attr_val` as-is or converted if required, or raise one of the [Attrs Types Exceptions](/api/attrs-types.md#attrs-types-exceptions) upon any failure.


> Some of Config Attrs are available but not supposed to be set by package Config, but still available to LIMP modules to access and read their values, which are:
## `debug`
The flag of whether debug options are active or not. It's not supposed to be set by a package, rather by the CLI. Default `False`.

## `env`
...

## `test`
The flag whether `test` workflow is active or not. If it's active it should be string representing the test name. It's not supposed to be set by a package, rather by the CLI. Default `False`.

## `test_flush`
The flag whether `test` workflow should flush and drop the previous test collections or simply continue with them. It's not supposed to be set by a package, rather by the CLI. Default `False`.

## `test_force`
The flag whether `test` workflow should break or force testing all steps after first failure. It's not supposed to be set by a package, rather by the CLI. Default `False`.

These config attrs are still available at public level so that your app can access them for various reasons and scenarios. For instance, your app can check whether `debug` options are active and print additional verbose messages, or whether `test` workflow is active and skip sending emails or SMSs as part of the modules methods.

## `test_env`
...

## `test_breakpoint`
...

## `_sys_docs`
...

## `_realms`
...

## `_cache`
...

## `_limp_version`
...