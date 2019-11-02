[Back to Index](/README.md)

> ⚠ Quick Start Article is derived from older version of the docs. Although, it has overall correct reference, areas related to using LIMP Sandbox and making calls are out-of-date.

# Quick Start
> Make sure you have MongoDB daemon working before proceeding. The daemon should accept connections on the hostname `localhost` on the default port `27017`. There should be no admin user created in order to allow LIMPd to create the database on your behalf. If any of these conditions don't apply in your case, go to the full [tutorial](/tutorial.md) which lets you create a package with the ability to connect to any `data_server`.

To begin with LIMP, clone [LIMP repo](https://github.com/masaar/limp) in your working directory. Next, clone [LIMP Sample App](https://github.com/masaar/limp-sample-app) into the `modules` folder, like:
```bash
git clone https://github.com/masaar/limp
cd limp/modules
git clone https://github.com/masaar/limp-sample-app
```

## Install Dependencies
Once both repos are cloned, you can install LIMP dependencies using the command:
```bash
python limpd.py --install-deps
```
Note that, LIMPd currently doesn't check the exit status of the `pip` commands executed, which means you have to check the console output yourself to confirm the installation of all the dependencies is successful. Once the process is done successfully you can run LIMPd using the following command:
```bash
python limpd.py --env dev --debug
```
If odds are in your favour (and ours) you should have this by the end of the output:
```log
2019-10-28 15:16:48,718  [INFO]  Welcome to LIMPd.
======== Running on http://0.0.0.0:8081 ========
```

# Under the Hood
When LIMPd runs, it connects to the `data_server` specified in https://github.com/masaar/limp-sample-app/__init__.py#L9 and then attempts to access https://github.com/masaar/limp-sample-app/__init__.py#L15 database. This behaviour is introduced in LIMPd for two reasons:
1. Confirm the `data` attrs are valid for when the app starts serving.
2. Create the necessary config collections and docs.

If you look at the full console output you should get:
```log
2019-10-28 15:16:44,331  [WARNING]  Port should be in integer format. Defaulting to 8081.
2019-10-28 15:16:44,928  [DEBUG]  Initialised module diff
2019-10-28 15:16:44,928  [DEBUG]  Initialised module notification
2019-10-28 15:16:44,929  [DEBUG]  Initialised module realm
2019-10-28 15:16:44,929  [DEBUG]  Initialised module session
2019-10-28 15:16:44,930  [DEBUG]  Initialised module setting
2019-10-28 15:16:44,930  [DEBUG]  Initialised module group
2019-10-28 15:16:44,931  [DEBUG]  Initialised module user
2019-10-28 15:16:44,931  [DEBUG]  Initialised module blog
2019-10-28 15:16:44,932  [DEBUG]  Initialised module blog_cat
2019-10-28 15:16:44,932  [DEBUG]  Initialised module staff
2019-10-28 15:16:45,397  [WARNING]  [SECURITY WARNING] Admin username is not explicitly set. It has been defaulted to '__ADMIN' but in production environment you should consider setting it to your own to protect your app from breaches.
2019-10-28 15:16:45,400  [WARNING]  [SECURITY WARNING] Admin email is not explicitly set. It has been defaulted to 'ADMIN@LIMP.MASAAR.COM' but in production environment you should consider setting it to your own to protect your app from breaches.
2019-10-28 15:16:45,404  [WARNING]  [SECURITY WARNING] Admin phone is not explicitly set. It has been defaulted to '+971500000000' but in production environment you should consider setting it to your own to protect your app from breaches.
2019-10-28 15:16:45,407  [WARNING]  [SECURITY WARNING] Admin password is not explicitly set. It has been defaulted to '__ADMIN' but in production environment you should consider setting it to your own to protect your app from breaches.
2019-10-28 15:16:45,409  [WARNING]  [SECURITY WARNING] Anon token is not explicitly set. It has been defaulted to '__ANON_TOKEN_f00000000000000000000012' but in production environment you should consider setting it to your own to protect your app from breaches.
2019-10-28 15:16:45,416  [DEBUG]  Testing realm mode.
2019-10-28 15:16:45,416  [DEBUG]  Testing users collection.
2019-10-28 15:16:45,418  [DEBUG]  Calling: user.read, with skip_events:['__PERM__', '__ON__'], query:[{'_id': 'f00000000000000000000010'}], doc.keys:dict_keys([])
2019-10-28 15:16:45,419  [DEBUG]  attempting to parse query: [{'_id': 'f00000000000000000000010'}]
2019-10-28 15:16:45,421  [DEBUG]  parsed query, aggregate_prefix: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}], aggregate_suffix: [{'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}], aggregate_match:[{'_id': ObjectId('f00000000000000000000010')}]
2019-10-28 15:16:45,423  [DEBUG]  aggregate_query: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000010')}}, {'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}]
2019-10-28 15:16:45,426  [DEBUG]  skip, limit, sort, group: None, None, {'_id': -1}, None.
2019-10-28 15:16:48,573  [DEBUG]  final query: AsyncIOMotorCollection(Collection(Database(MongoClient(host=['localhost:27017'], document_class=dict, tz_aware=False, connect=True, ssl=False, driver=DriverInfo(name='Motor', version='2.0.0', platform=None)), 'limp_data'), 'users')), [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000010')}}, {'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}, {'$sort': {'_id': -1}}].
2019-10-28 15:16:48,586  [DEBUG]  Call results: {"status": 200, "msg": "Found 1 docs.", "args": {"total": 1, "count": 1, "docs": [{"_id": "f00000000000000000000010", "name": {"ar_AE": "__ADMIN", "en_AE": "__ADMIN"}, "locale": "ar_AE", "create_time": "2019-08-14T08:02:54.035482", "login_time": "2019-09-13T15:54:18.672897", "groups": [], "privileges": {"*": "*"}, "status": "active", "attrs": {}}], "groups": {}}}
2019-10-28 15:16:48,589  [DEBUG]  Calling: user.read, with skip_events:['__PERM__', '__ON__'], query:[{'_id': 'f00000000000000000000011'}], doc.keys:dict_keys([])
2019-10-28 15:16:48,591  [DEBUG]  attempting to parse query: [{'_id': 'f00000000000000000000011'}]
2019-10-28 15:16:48,592  [DEBUG]  parsed query, aggregate_prefix: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}], aggregate_suffix: [{'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}], aggregate_match:[{'_id': ObjectId('f00000000000000000000011')}]
2019-10-28 15:16:48,595  [DEBUG]  aggregate_query: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000011')}}, {'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}]
2019-10-28 15:16:48,598  [DEBUG]  skip, limit, sort, group: None, None, {'_id': -1}, None.
2019-10-28 15:16:48,600  [DEBUG]  final query: AsyncIOMotorCollection(Collection(Database(MongoClient(host=['localhost:27017'], document_class=dict, tz_aware=False, connect=True, ssl=False, driver=DriverInfo(name='Motor', version='2.0.0', platform=None)), 'limp_data'), 'users')), [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000011')}}, {'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}, {'$sort': {'_id': -1}}].
2019-10-28 15:16:48,607  [DEBUG]  Call results: {"status": 200, "msg": "Found 1 docs.", "args": {"total": 1, "count": 1, "docs": [{"_id": "f00000000000000000000011", "name": {"ar_AE": "__ANON", "en_AE": "__ANON"}, "locale": "ar_AE", "create_time": "2019-08-14T08:02:54.095485", "login_time": null, "groups": [], "privileges": {}, "status": "active", "attrs": {}}], "groups": {}}}
2019-10-28 15:16:48,609  [DEBUG]  Testing sessions collection.
2019-10-28 15:16:48,609  [DEBUG]  Calling: session.read, with skip_events:['__PERM__', '__ON__'], query:[{'_id': 'f00000000000000000000012'}], doc.keys:dict_keys([])
2019-10-28 15:16:48,610  [DEBUG]  attempting to parse query: [{'_id': 'f00000000000000000000012'}]
2019-10-28 15:16:48,611  [DEBUG]  parsed query, aggregate_prefix: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}], aggregate_suffix: [{'$project': {'_id': '$_id', 'user': '$user', 'host_add': '$host_add', 'user_agent': '$user_agent', 'timestamp': '$timestamp', 'expiry': '$expiry', 'token': '$token'}}], aggregate_match:[{'_id': ObjectId('f00000000000000000000012')}]
2019-10-28 15:16:48,612  [DEBUG]  aggregate_query: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000012')}}, {'$project': {'_id': '$_id', 'user': '$user', 'host_add': '$host_add', 'user_agent': '$user_agent', 'timestamp': '$timestamp', 'expiry': '$expiry', 'token': '$token'}}] 2019-10-28 15:16:48,614  [DEBUG]  skip, limit, sort, group: None, None, {'_id': -1}, None.
2019-10-28 15:16:48,626  [DEBUG]  final query: AsyncIOMotorCollection(Collection(Database(MongoClient(host=['localhost:27017'], document_class=dict, tz_aware=False, connect=True, ssl=False, driver=DriverInfo(name='Motor', version='2.0.0', platform=None)), 'limp_data'), 'sessions')), [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000012')}}, {'$project': {'_id': '$_id', 'user': '$user', 'host_add': '$host_add', 'user_agent': '$user_agent', 'timestamp': '$timestamp', 'expiry': '$expiry', 'token': '$token'}}, {'$sort': {'_id': -1}}].
2019-10-28 15:16:48,632  [DEBUG]  Calling: user.read, with skip_events:['__PERM__'], query:[{'_id': ObjectId('f00000000000000000000011')}], doc.keys:dict_keys([])
2019-10-28 15:16:48,633  [DEBUG]  attempting to parse query: [{'_id': ObjectId('f00000000000000000000011')}]
2019-10-28 15:16:48,634  [DEBUG]  parsed query, aggregate_prefix: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}], aggregate_suffix: [{'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}], aggregate_match:[{'_id': ObjectId('f00000000000000000000011')}]
2019-10-28 15:16:48,637  [DEBUG]  aggregate_query: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000011')}}, {'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}]
2019-10-28 15:16:48,639  [DEBUG]  skip, limit, sort, group: None, None, {'_id': -1}, None.
2019-10-28 15:16:48,641  [DEBUG]  final query: AsyncIOMotorCollection(Collection(Database(MongoClient(host=['localhost:27017'], document_class=dict, tz_aware=False, connect=True, ssl=False, driver=DriverInfo(name='Motor', version='2.0.0', platform=None)), 'limp_data'), 'users')), [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000011')}}, {'$project': {'_id': '$_id', 'name': '$name', 'locale': '$locale', 'create_time': '$create_time', 'login_time': '$login_time', 'groups': '$groups', 'privileges': '$privileges', 'status': '$status', 'attrs': '$attrs'}}, {'$sort': {'_id': -1}}].
2019-10-28 15:16:48,651  [DEBUG]  Call results: {"status": 200, "msg": "Found 1 docs.", "args": {"total": 1, "count": 1, "docs": [{"_id": "f00000000000000000000011", "name": {"ar_AE": "__ANON", "en_AE": "__ANON"}, "locale": "ar_AE", "create_time": "2019-08-14T08:02:54.095485", "login_time": null, "groups": [], "privileges": {}, "status": "active", "attrs": {}}], "groups": {}}}
2019-10-28 15:16:48,655  [DEBUG]  Call results: {"status": 200, "msg": "Found 1 docs.", "args": {"total": 1, "count": 1, "docs": [{"_id": "f00000000000000000000012", "user": {"_id": "f00000000000000000000011", "name": {"ar_AE": "__ANON", "en_AE": "__ANON"}, "locale": "ar_AE", "create_time": "2019-08-14T08:02:54.095485", "login_time": null, "groups": [], "privileges": {}, "status": "active", "attrs": {}}, "host_add": "127.0.0.1", "user_agent": "__ANON_TOKEN_f00000000000000000000012", "timestamp": "1970-01-01T00:00:00", "expiry": "1970-01-01T00:00:00", "token": "__ANON_TOKEN_f00000000000000000000012"}], "groups": {}}}
2019-10-28 15:16:48,657  [DEBUG]  Testing groups collection.
2019-10-28 15:16:48,658  [DEBUG]  Calling: group.read, with skip_events:['__PERM__', '__ON__'], query:[{'_id': 'f00000000000000000000013'}], doc.keys:dict_keys([])
2019-10-28 15:16:48,658  [DEBUG]  attempting to parse query: [{'_id': 'f00000000000000000000013'}]
2019-10-28 15:16:48,660  [DEBUG]  parsed query, aggregate_prefix: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}], aggregate_suffix: [{'$project': {'_id': '$_id', 'user': '$user', 'name': '$name', 'bio': '$bio', 'privileges': '$privileges', 'attrs': '$attrs'}}], aggregate_match:[{'_id': ObjectId('f00000000000000000000013')}] 2019-10-28 15:16:48,661  [DEBUG]  aggregate_query: [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000013')}}, {'$project': {'_id': '$_id', 'user': '$user', 'name': '$name', 'bio': '$bio', 'privileges': '$privileges', 'attrs': '$attrs'}}]
2019-10-28 15:16:48,662  [DEBUG]  skip, limit, sort, group: None, None, {'_id': -1}, None.
2019-10-28 15:16:48,674  [DEBUG]  final query: AsyncIOMotorCollection(Collection(Database(MongoClient(host=['localhost:27017'], document_class=dict, tz_aware=False, connect=True, ssl=False, driver=DriverInfo(name='Motor', version='2.0.0', platform=None)), 'limp_data'), 'groups')), [{'$match': {'$or': [{'__deleted': {'$exists': False}}, {'__deleted': False}]}}, {'$match': {'_id': ObjectId('f00000000000000000000013')}}, {'$project': {'_id': '$_id', 'user': '$user', 'name': '$name', 'bio': '$bio', 'privileges': '$privileges', 'attrs': '$attrs'}}, {'$sort': {'_id': -1}}].
2019-10-28 15:16:48,684  [DEBUG]  Call results: {"status": 200, "msg": "Found 1 docs.", "args": {"total": 1, "count": 1, "docs": [{"_id": "f00000000000000000000013", "user": "f00000000000000000000010", "name": {"ar_AE": "__DEFAULT", "en_AE": "__DEFAULT"}, "bio": {"ar_AE": "__DEFAULT", "en_AE": "__DEFAULT"}, "privileges": {}, "attrs": {}}], "groups": {}}}
2019-10-28 15:16:48,684  [DEBUG]  Testing app-specific groups collection.
2019-10-28 15:16:48,684  [DEBUG]  Testing data indexes
2019-10-28 15:16:48,685  [DEBUG]  Creating '__deleted' data indexes for all collections.
2019-10-28 15:16:48,686  [DEBUG]  Attempting to create '__deleted' data index for collection: diff
2019-10-28 15:16:48,686  [DEBUG]  Attempting to create '__deleted' data index for collection: notifications
2019-10-28 15:16:48,687  [DEBUG]  Attempting to create '__deleted' data index for collection: sessions
2019-10-28 15:16:48,687  [DEBUG]  Attempting to create '__deleted' data index for collection: settings
2019-10-28 15:16:48,688  [DEBUG]  Attempting to create '__deleted' data index for collection: groups
2019-10-28 15:16:48,689  [DEBUG]  Attempting to create '__deleted' data index for collection: users
2019-10-28 15:16:48,690  [DEBUG]  Attempting to create '__deleted' data index for collection: blogs
2019-10-28 15:16:48,692  [DEBUG]  Attempting to create '__deleted' data index for collection: blogs_cats
2019-10-28 15:16:48,693  [DEBUG]  Attempting to create '__deleted' data index for collection: staff
2019-10-28 15:16:48,694  [DEBUG]  Testing docs.
2019-10-28 15:16:48,694  [DEBUG]  Loaded modules: {'diff': {'user': 'id', 'module': 'str', 'doc': 'id', 'vars': 'attrs', 'remarks': 'str', 'create_time': 'datetime'}, 'notification': {'user': 'id', 'create_time': 'datetime', 'notify_time': 'datetime', 'title': 'str', 'content': 'id', 'status': {'snooze', 'new', 'done'}}, 'session': {'user': 'id', 'host_add': 'ip', 'user_agent': 'str', 'timestamp': 'datetime', 'expiry': 'datetime', 'token': 'str'}, 'setting': {'user': 'id', 'var': 'str', 'val': 'any', 'type': {'global', 'user'}}, 'group': {'user': 'id', 'name': 'locale', 'bio': 'locale', 'privileges': 'privileges', 'attrs': 'attrs'}, 'user': {'name': 'locale', 'locale': 'locales', 'create_time': 'datetime', 'login_time': 'datetime', 'groups': ['id'], 'privileges': 'privileges', 'status': {'banned', 'disabled_password', 'deleted', 'active'}, 'attrs': 'attrs'}, 'blog': {'user': 'id', 'status': {'published', 'rejected', 'pending', 'draft'}, 'title': 'locale', 'subtitle': 'locale', 'permalink': 'str', 'content': 'locale', 'tags': ['str'], 'cat': 'id', 'access': 'access', 'create_time': 'datetime'}, 'blog_cat': {'user': 'id', 'title': 'locale', 'desc': 'locale'}, 'staff': {'user': 'id', 'photo': 'file', 'name': 'locale', 'jobtitle': 'locale', 'bio': 'locale', 'create_time': 'datetime'}}
2019-10-28 15:16:48,704  [DEBUG]  Config has attrs: {'debug': 'True', 'env': 'dev', 'version': '5.8', 'test': 'None', 'test_flush': 'False', 'test_force': 'False', 'test_env': 'False', 'test_breakpoint': 'False', 'test_collections': 'False', 'tests': "{'auth_as_admin': [{'step': 'auth', 'var': 'email', 'val': 'ADMIN@LIMP.MASAAR.COM', 'hash': 'eyJoYXNoIjpbImVtYWlsIiwiQURNSU5ATElNUC5NQVNBQVIuQ09NIiwiX19BRE1JTiIsIl9fQU5PTl9UT0tFTl9mMDAwMDAwMDAwMDAwMDAwMDAwMDAwMTIiXX0'}], 'create_blog_cat': [{'step': 'test', 'test': 'auth_as_admin'}, {'step': 'call', 'module': 'blog_cat', 'method': 'create', 'query': [], 'doc': {'title': {'__attr': 'locale'}, 'desc': {'__attr': 'locale'}}, 'acceptance': {'status': 200}}, {'step': 'signout'}, {'step': 'call', 'module': 'blog_cat', 'method': 'read', 'query': [], 'doc': {}, 'acceptance': {'status': 200, 'args.count': 1}}], 'create_blog_post': [{'step': 'test', 'test': 'create_blog_cat'}, {'step': 'test', 'test': 'auth_as_admin'}, {'step': 'call', 'module': 'blog', 'method': 'create', 'query': [], 'doc': {'status': 'published', 'title': {'__attr': 'locale'}, 'content': {'__attr': 'locale'}, 'tags': [{'__attr': 'str', 'count': 5}], 'cat': '$__steps:0.steps:1.results.args.docs:0._id'}, 'acceptance': {'status': 200}}, {'step': 'call', 'module': 'blog', 'method': 'create', 'query': [], 'doc': {'status': 'draft', 'title': {'__attr': 'locale'}, 'content': {'__attr': 'locale'}, 'tags': [{'__attr': 'str', 'count': 5}], 'cat': '$__steps:0.steps:1.results.args.docs:0._id'}, 'acceptance': {'status': 200}}, {'step': 'call', 'module': 'blog', 'method': 'read', 'query': [], 'doc': {}, 'acceptance': {'status': 200, 'args.count': 2}}, {'step': 'signout'}, {'step': 'call', 'module': 'blog', 'method': 'read', 'query': [], 'doc': {}, 'acceptance': {'status': 200, 'args.count': 1}}]}", 'emulate_test': 'False', 'realm': 'False', 'vars': '{}', 'conn_timeout': '600', 'quota_anon_min': '40', 'quota_auth_min': '100', 'quota_ip_min': '500', 'data_server': 'mongodb://localhost', 'data_name': 'limp_data', 'data_ssl': 'False', 'data_ca_name': 'None', 'data_ca': 'None', 'data_azure_mongo': 'False', 'email_auth': '{}', 'locales': "['ar_AE', 'en_AE']", 'locale': 'ar_AE', 'admin_username': '__ADMIN', 'admin_email': 'ADMIN@LIMP.MASAAR.COM', 'admin_phone': '+971500000000', 'admin_password': '__ADMIN', 'anon_token': '__ANON_TOKEN_f00000000000000000000012', 'anon_privileges': '{}', 'user_attrs': "{'auth_attr': 'str'}", 'user_auth_attrs': "['auth_attr']", 'user_attrs_defaults': '{}', 'groups': '[]', 'default_privileges': '{}', 'data_indexes': '[]', 'docs': '[]', 'l10n': '{}', 'jobs': '[]', 'gateways': '{}', 'types': '{}'}
2019-10-28 15:16:48,714  [DEBUG]  Generated get_routes: ['/setting/retrieve_file/{_id}/{attr}/{filename}', '/setting/retrieve_file/{_id}/{attr}/{thumb}/{filename}', '/staff/retrieve_file/{_id}/{attr}/{filename}', '/staff/retrieve_file/{_id}/{attr}/{thumb}/{filename}']
2019-10-28 15:16:48,715  [DEBUG]  Generated post_routes: []
2019-10-28 15:16:48,718  [INFO]  Welcome to LIMPd.
======== Running on http://0.0.0.0:8081 ========
(Press CTRL+C to quit)
```
Let's go through the main points:
1. LIMPd checks if app is running in [realm](/realm.md) mode.
2. LIMPd checks if app is running on Azure by confirming `data_azure_mongo` mode.
3. LIMPd checks `users` collection, and creates `ADMIN` and `ANON` users if not present.
4. LIMPd checks `sessions` collection, and creates `ANON` session required to receive and accept calls from non-authenticated users.
5. LIMPd checks `groups` collection, and creates `DEFAULT` group required to set the `default_privileges` of the users.
6. LIMPd checks loaded config `groups` and creates them.
7. LIMPd checks loaded config `data_indexes` and creates them.
8. LIMPd checks loaded config `docs` and creates them.
9. Once all previous checks are done, LIMP would be ready ro serve connections on `http://localhost:8081` for `HTTP/1 GET, POST` interfaces, and `ws://localhost:8081/ws` for `HTTP/2 Websocket` interface.

# Interacting with LIMP
To start interacting with `limp-sample-app` you just run, go to [LIMP Sandbox on Github](https://masaar.github.io/limp-sandbox/dist/limp-sandbox/). Which is a tool we originally built to test early versions of [LIMP SDK for Angular](https://github.com/masaar/ng-limp), but continued to be develop as standalone sandbox playground.

To begin using LIMP Sandbox, from first panel `SDK Init` click on `init()` button, which would connect to LIMP on the specified `API URI` using `API Anon Token`. Note that in Firefox we observed the behaviour where the browser would refuse to connect to local websockets served over the insecure `ws` protocol. If you are on Firefox, use any Chromium-based browser instead. If you see a successful connection message in the output area then, congrats! Your setup is working. Then you can start by sending an `auth` (_authentication_) call using the default credentials for the `ADMIN` user using:
```
ADMIN@LIMP.MASAAR.COM
__ADMIN
```
You should see a new message in the output indicating that you were `authed` (_authenticated_) as well as the session data. Following you can make some calls to your app using the `SDK Call` panel. For instance you can query all the users by passing the following values:
```
endpoint: user/read
query: []
doc: {}
```
This should give you additional messages in the output with two users: `ADMIN` and `ANON` users. To query a specific user, pass its `_id` value as a query param `_id`.

Since you are using `limp-sample-app` you should explore the following modules and endpoints:

## Introduction
Our `limp-sample-app` is an app representing a company website. It has a blog that is served and managed using `Blog` and `BlogCat` modules, as well as staff directory served and managed using `Staff` module.

## Staff
To begin with this module, we would explore the four operations of `CRUD`:

### Create
To create a new staff doc, or any docs at all in the LIMP ecosystem, you call the module `create` method using the endpoint `staff/create`.

Start by setting `Endpoint` in `SDK Call` to `staff/create`. Next Start adding the following `doc` attrs using the `+` button next to `Doc`. LIMP Sandbox has the ability to allow developers to add multiple attrs at once, either in the `doc` or `query` object. After you click on `+` button you would be greeted with a prompt box asking you the names of the attrs you want to add. Copy and paste in the prompt box the following: `photo,name,jobtitle,bio` and then click on `Ok`. You would notice new four fields are now present under the `Doc` section of `SDK Call` panel.

Change attr `photo` type to `file` from the select menu before the text input. All other fields should be changed to type `locale`. These types are just example of how much LIMP is powerful is it allows you to deal with all data types without being worried at all about how your app has to deal with them. In part this is possible because `HTTP/2 Websocket` protocol allows typed-JSON data to be transmitted bi-directionally, but also because LIMP has sophisticated workflow to handle data types.

Once you change the types you would notice `photo` attr field is now a file input, while other attrs are having two input fields each; `val.ar_AE` and `val.en_AE`. Since LIMP was developed by Masaar which is serving customers with multi-language requirements, this feature was built right in the core of LIMP. You can learn more about such features by referring to [Apps Localisation](/apps-localisation.md). Now let's create the first staff by inputting some data in all the attrs, and then click on `call()`. Make sure you have already been `authed` (_authenticated_) as `ADMIN` as currently there's no other user which has the [privilege](/tutorial.md#privileges) to create staff docs. If the call is successful you would get `Created 1 docs.` message. Repeat the same steps again with other set of details to create another staff doc.

### Read
Similar to `create` operation, LIMP follows and has `read` method on any module which had it enabled. Set `Endpoint` to `staff/read`, remove all the doc attrs and click on `call()`. You should receive `Found 2 docs.` message response. If you attempt to expand the JSON tree viewer, you would find both the docs in `args.docs`. That's how LIMP messages are always structured--Any matched data is always sent as part of the `args` object in the response. Now, to read specifically either of the staff docs, all you have to do is click on `+` button next to `Query` and type `_id` in the prompt box. This would create a `query` object arg `_id` that you see present under `Query`. Copy one of the `_id`s of the two docs and paste it in the `_id` text input, and click `call()`. If you copied that correctly you should receive `Found 1 docs.` message response with the details of that doc. Now you know how to query all docs in any module, or selectively query them. You can read more about [query object](/tutorial.md#query-object) in the tutorial.

One last thing, we uploaded a photo for the staff, so how can we get it? For many technical reasons we resided on stripping any files from the response of any call. And, to get those files `HTTP/1 GET` interface is present. In our `Staff` module case you have the following link scheme available:
```
http://localhost:8081/staff/retrieve_file/{_id}/photo/{file_name}
```
This scheme is a public scheme available for any module to use. You can learn more about it in [retrieve_file method](/tutorial.md#retrieve_file-method) section in the tutorial. For instance, copy either of the `_id` of the two created docs, and replace `{_id}` with that value, and similarly replace `{file_name}` with the photo file name. This scheme checks the file name when retrieving the photo, so if the name is not matching you would get `{"status": 404, "msg": "Requested content not found."}` in your browser. If the values are correct you would be presented with the photo you uploaded.

### Update
To update either of the staff docs simply use the LIMP ecosystem `update` method--Use the following details in `SDK Call` panel:
```
endpoint: staff/update
query: [{_id: 'staff doc _id'}]
doc: {attr_name: 'new_value'}
```
If the previous snippet is not clear enough, the idea is you can `update` any doc using any module `update` method, by simply passing `_id` of the doc you are looking to update and the attrs value you would like to change. Notice that you don't have to send the full doc again, just the attrs you want to change its value.

### Delete
To delete either of the docs your call should be:
```
endpoint: staff/delete
query: [{_id: 'staff doc _id'}]
```

## Blog
Blog and BlogCat module are having the same identical `read`, `create`, `update` and `delete` methods to both modules. The only difference here is that `Blog` and `BlogCat` modules are linked--Every blog doc is linked to a blog_cat doc. It's the same structure you get on any blogging platform and/or software. For that you need to create the blog_cat first, take its `_id` and give it to a blog you want to create.

For starter create your blog_cat using the following call:
```
endpoint: blog_cat/create
doc: title[;locale title], desc[;locale desc]
```
Keep the `_id` of this category handy.

Then, let's create a blog doc, using the call:
```
endpoint: blog/create
doc: {title:'locale title', content:'locale content', cat:'blog cat _id'}
```
If the `_id` is wrong by any chance, your would get an error response telling you `Invalid BlogCat`. If everything is good you would get `Created 1 docs.` response.

Now try to read the blog you created using endpoint `blog/read` with no `query` or `doc` args. What you would get is what you assume the blog doc, but have a deep look at `cat` attr. What do you get? Rather than the `_id` of the blog_cat, LIMP dynamically extended this attr and set it to the blog_cat doc value so you can easily get the blog_cat name and desc to present in your app. Thanks to our [extns](/api-call.md#extns) workflow, you can easily extend any attr in your module using any other module doc, simply by having its `_id` set in its value.

This wraps up the quick start guide. You can explore the `limp-sample-app` source code and fiddle with it to get some interesting new creations of yours. Or, continue to our full and extended [tutorial](/tutorial.md).