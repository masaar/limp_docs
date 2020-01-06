[Back to Core Package Index](./README.md)

### Module: Diff
`Diff` module provides data type and controller for `Diff Workflow`. It is meant for use by internal calls only. Best practice to accessing diff docs is by creating proxy modules or writing LIMP methods that expose the diff docs.
#### Attrs
* user:
  * `_id` of `User` doc the doc belongs to.
  * Type: `<ATTR:ID,{}>`
* module:
  * Name of the module the original doc is part of.
  * Type: `<ATTR:STR,{'pattern': None}>`
* doc:
  * `_id` of the original doc.
  * Type: `<ATTR:ID,{}>`
  * Default [doc]: None
* vars:
  * Key-value `dict` containing all attrs that have been updated from the original doc.
  * Type: `<ATTR:DICT,{'dict': {'__key': <ATTR:STR,{'pattern': None}>, '__val': <ATTR:ANY,{}>}}>`
* remarks:
  * Human-readable remarks of the doc. This is introduced to allow developers to add log messages to diff docs.
  * Type: `<ATTR:STR,{'pattern': None}>`
  * Default [remarks]: 
* create_time:
  * Python `datetime` ISO format of the doc creation.
  * Type: `<ATTR:DATETIME,{'ranges': None}>`
#### Methods
##### Method: read
* Permissions Sets:
  * read
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
##### Method: create
* Permissions Sets:
  * __sys
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
##### Method: delete
* Permissions Sets:
  * delete
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
#### Extended Attrs: None
#### Cache Sets: None
#### Analytics Sets: None