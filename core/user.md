[Back to Core Package Index](./README.md)

# Module: User
`User` module provides data type and controller for users in LIMP eco-system. This module is supposed to be used for internal calls only, however it has wide-access permissions in order to allow admins, proxy modules to easily expose the methods.
## Attrs
* name:
  * Name of the user as `LOCALE`.
  * Type: `<ATTR:LOCALE,{}>`
* locale:
  * Default locale of the user.
  * Type: `<ATTR:LOCALES,{}>`
  * Default [locale]: ar_AE
* create_time:
  * Python `datetime` ISO format of the doc creation.
  * Type: `<ATTR:DATETIME,{'ranges': None}>`
* login_time:
  * Python `datetime` ISO format of the last login.
  * Type: `<ATTR:DATETIME,{'ranges': None}>`
  * Default [login_time]: None
* groups:
  * List of `_id` for every group the user is member of.
  * Type: `<ATTR:LIST,{'list': [<ATTR:ID,{}>], 'min': None, 'max': None}>`
  * Default [groups]: []
* privileges:
  * Privileges of the user. These privileges are always available to the user regardless of whether groups user is part of have them or not.
  * Type: `<ATTR:DICT,{'dict': {'__key': <ATTR:STR,{'pattern': None}>, '__val': <ATTR:LIST,{'list': [<ATTR:STR,{'pattern': None}>], 'min': None, 'max': None}>}}>`
  * Default [privileges]: {}
* status:
  * Status of the user to determine whether user has access to the app or not.
  * Type: `<ATTR:LITERAL,{'literal': ['active', 'banned', 'deleted', 'disabled_password']}>`
  * Default [status]: active
## Methods
### Method: read
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier: None
  * read
	* Query Modifier:
	  * Set 0:
		* _id: $__user
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: create
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: update
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier:
	  * Set 0:
		* groups: None
		* user: None
		* create_time: None
  * update
	* Query Modifier:
	  * Set 0:
		* _id: $__user
	* Doc Modifier:
	  * Set 0:
		* groups: None
		* privileges: None
		* user: None
		* create_time: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
### Method: delete
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier: None
  * delete
	* Query Modifier:
	  * Set 0:
		* _id: $__user
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
### Method: read_privileges
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier: None
  * read
	* Query Modifier:
	  * Set 0:
		* _id: $__user
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
### Method: add_group
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* DOC Args Sets:
  * `{'group': <ATTR:ID,{}>}`
  * `{'group': <ATTR:LIST,{'list': [<ATTR:ID,{}>], 'min': None, 'max': None}>}`
### Method: delete_group
* Permissions Sets:
  * admin
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>, 'group': <ATTR:ID,{}>}`
* Doc Args Sets: None
### Method: retrieve_file
* Permissions Sets:
  * __sys
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>, 'attr': <ATTR:STR,{'pattern': None}>, 'filename': <ATTR:STR,{'pattern': None}>}`
  * `{'_id': <ATTR:ID,{}>, 'attr': <ATTR:STR,{'pattern': None}>, 'thumb': <ATTR:STR,{'pattern': '[0-9]+x[0-9]+'}>, 'filename': <ATTR:STR,{'pattern': None}>}`
* Doc Args Sets: None
### Method: create_file
* Permissions Sets:
  * __sys
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>, 'attr': <ATTR:STR,{'pattern': None}>}`
* DOC Args Sets:
  * `{'file': <ATTR:FILE,{'types': None, 'max_ratio': None, 'min_ratio': None, 'max_dims': None, 'min_dims': None, 'max_size': None}>}`
### Method: delete_file
* Permissions Sets:
  * __sys
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>, 'attr': <ATTR:STR,{'pattern': None}>, 'index': <ATTR:INT,{'range': None}>, 'name': <ATTR:STR,{'pattern': None}>}`
* Doc Args Sets: None
## Extended Attrs: None
## Cache Sets: None
## Analytics Sets: None