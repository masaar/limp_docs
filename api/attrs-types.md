# Attrs Types
Attrs Types are used to automate the process of data validation for LIMP apps. In most it's used with (calls `doc`)[/api/call.md#doc] to methods, but also can be used to validate (GET methods `query`)[/api/method.md#get-methods].

## Built-in Attrs Types
LIMP has huge set of built-in Attrs Types that cover most of the data validation purposes. These Attrs Types can be customised for more spcific validation process.

### `any`
An attr with this type means it can have any value, ultimately skipping type-check on it altogether.

### `id`
An attr with this type means it has to have `BSON ObjectId`. This is usually the type set for attr that has the `_id` value of another doc from the same module or another. LIMP type-check step for this type includes converting `str` type to `BSON ObjectId` if valid, allowing developers to pass `id` as `str`.

### `str`
Self-descriptive string type. Accepts anything that is a string.

#### `str[PATTERN]`
Type `str` allows developers to force custom type-check by appending a Python format regexp in square brackets to force specific pattern check. e.g. `str[[a-zA-Z]{2,4}]`.

### `int`
Self-descriptive integer type. Accepts anything that is an integer.

#### `int[BEGIN:END:STEP]`
Type `int` allows developers to force custom range type-check by appending two required `BEGIN` and `END`, as well optional `STEP` values in square brackets, all separated by colons. This is Python range generation step, meaning `BEGIN` is inclusive, but `END` is exclusive. e.g. `int[1:10]` matches anything from inclusive `1` to exclusive `10`, and `int[0:11:2]` matches all even numbers from `1` to `10` all-inclusive.

### `bool`
Self-descriptive boolean type. Accepts anything that is a boolean.

### `locale`
An attr with this type means it's Python `dict` with multiple values, each representing a supported locale in LIMP app.

### `locales`
An attr with this type means it's a `str` with the accepted value being one of the supported locales in LIMP app.

### `email`
Self-descriptive email type. Accepts a string that matches the regexp `r'[^@]+@[^@]+\.[^@]+'` in Python.

### `phone`
Self-descriptive phone type. Accepts a string that matches the regexp `r'\+[0-9]+'` in Python.

#### `phone[CODE, CODE...,CODE]`
Type `phone` allows developers to set specfic accepted codes for `phone` attr by appending comma-separated codes in square brackets. e.g. `phone[123,456,789,0]` matches any phone which has either of the codes `123`, `456`, `789` or `0`.

### `uri:web`
Self-descriptive web URI type. Accepts a string that matches the regexp `r'https?:\/\/(?:[\w\-\_]+\.)(?:\.?[\w]{2,})+$'` in Python.

### `datetime`
Self-descriptive datetime type. Accepts Python ISO format `datetime` value which matches the regexp `r'^[0-9]{4}-[0-9]{2}-[0-9]{2}T[0-9]{2}:[0-9]{2}:[0-9]{2}(\.[0-9]{6})?$'`.

### `date`
Self-descriptive date type. Accepts Python ISO format `date` value `r'^[0-9]{4}-[0-9]{2}-[0-9]{2}$'`.

### `time`
Self-descriptive time type. Accepts Python ISO format `time` value which matches the regexp `r'^[0-9]{2}:[0-9]{2}(:[0-9]{2}(\.[0-9]{6})?)?$'`.

### `file`
Self-descriptive file type. Accepts a Python `dict` that has the file attrs as required by LIMP which are: `name`, `size`, `type`, `lastModified` and `content`.

#### `file[TYPE,TYPE...,TYPE]`
Type `file` allows developers to specify list of accepted file MIME types for the attr by appending comma-separated list of MIME types in squeare brackets. e.g. `file[image/*,video/*]` to allow all files which are `image` and `video`, or `file[image/jpeg]` to allow only JPEG images.

### `geo`
A GeoJSON-compatible type. This is essentially for use with MongoDB `$geo` features.

### `Options`
Type `Options` is used to define set of options for the attr as Python Tuple. Any other value not from the tuple would be considered wrong value. e.g. `shipment` module with attr `status` can have the type tuple as `('at-warehouse', 'shipped', 'received', 'cancelled')`.

### `List`
Type `List` is used to define list of other Attr Type. e.g. `blog` module, can have the `tag` attr set to `['str']` to flag that it accepts list of strings. You can pass more than one type in the list to allow multiple types.

### `attrs`
Type `attrs` accepts Python `dict`. This is used when you need complex data types of your definition. Developers would have to type-check attrs set to `attrs` on their own.

### `Dict`
Type `Dict` matches native Python `dict` type. You can use this as a value if you want more control over `attrs` type. Developers can pass child attrs and their respective types from built-in Attrs Types.


## App-specific Attrs Types
Developers can define LIMP apps-specific Attrs Types as part of (pacakges)[/api/package.md] (configs)[/api/config.md]. Attrs Types should go along (`types` Config Attr)[/api/config.md#types] as Python `dict`, with the keys being the Attrs Types, and values being Python `callables` that returns the value as-is or converted, or raises one of the [Attrs Types Exceptions](#attrs-types-exceptions).

## Attrs Types Exceptions
The sequence of data validation and type-check in LIMP works using two functions located in `utils` Python module of LIMP. The functions are `validate_doc`, and `validate_attr`. At the event of any failure these functions would raise one of the three Attrs Types Exceptions:

### MissingAttrException
In cases where LIMP is matching set of data against (`Attrs`)[/api/module.md#attrs] or (GET methods `query_args`)[/api/method.md#query_args] that require all `attrs` to be defined, if any is missing exception `MissingAttrException` would be raised. The exception has only one attribute `attr_name` which can be used to determine which `attr` is missing.

### InvalidAttrException
In case where LIMP find a type mismatch, exception `InvalidAttrException` would be raised. The exception has three attributes `attr_name`, `attr_type`, `val_type` which respectively refer to `attr` name, expected type, and actual value of the `attr`.

### ConvertAttrException
In few cases, LIMP would accept a type as another and converts it. This was introduced to allow developers from easily passing data types that might be not possible to via (requests)[/api/request.md], mainly for binary data. e.g. this allows LIMP to validate `attr` of (type `id`)[#id] as `str` value and converts it to `BSON ObjectId`. If the passed value is of the acceptable type, i.e. `str`, but failed to convert to actual type, i.e. `id`, exception `ConvertAttrException` would be raised. The exception has three attributes `attr_name`, `attr_type`, `val_type` which respectively refer to `attr` name, expected type, and actual value of the `attr`.