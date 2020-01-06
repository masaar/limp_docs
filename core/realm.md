[Back to Core Package Index](./README.md)

### Module: Realm
`Realm` module module provides data type and controller for Realm Mode in LIMP eco-system.
#### Attrs
* user:
  * `_id` of `User` doc the doc belongs to. This is also the ADMIN of the realm.
  * Type: `<ATTR:ID,{}>`
* name:
  * Name of the realm. This is both readable as well as unique name.
  * Type: `<ATTR:STR,{'pattern': None}>`
* default:
  * `_id` of `Group` doc that serves as `DEFAULT` group of the realm.
  * Type: `<ATTR:ID,{}>`
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
  * create
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
##### Method: update
* Permissions Sets:
  * update
	* Query Modifier: None
	* Doc Modifier:
	  * Set 0:
		* user: None
		* create_time: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
##### Method: delete
* Permissions Sets:
  * delete
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
#### Extended Attrs: None
#### Cache Sets: None
#### Analytics Sets: None