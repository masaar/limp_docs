[Back to Core Package Index](./README.md)

# Module: Group
`Group` module provides data type and controller for groups in LIMP eco-system.
## Attrs
* user:
  * `_id` of `User` doc the doc belongs to.
  * Type: `<ATTR:ID,{}>`
* name:
  * Name of the groups as `LOCALE`.
  * Type: `<ATTR:LOCALE,{}>`
* desc:
  * Description of the group as `LOCALE`. This can be used for dynamic generated groups that are meant to be exposed to end-users.
  * Type: `<ATTR:LOCALE,{}>`
  * Default [desc]: {'ar_AE': '', 'en_AE': ''}
* privileges:
  * Privileges that any user is a member of the group has.
  * Type: `<ATTR:DICT,{'dict': {'__key': <ATTR:STR,{'pattern': None}>, '__val': <ATTR:LIST,{'list': [<ATTR:STR,{'pattern': None}>], 'min': None, 'max': None}>}}>`
  * Default [privileges]: {}
* settings:
  * `Setting` docs to be created, or required for members users when added to the group.
  * Type: `<ATTR:DICT,{'dict': {'__key': <ATTR:STR,{'pattern': None}>, '__val': <ATTR:ANY,{}>}}>`
  * Default [settings]: {}
* create_time:
  * Python `datetime` ISO format of the doc creation.
  * Type: `<ATTR:DATETIME,{'ranges': None}>`
## Methods
### Method: read
* Permissions Sets:
  * admin
	* Query Modifier: None
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
		* user: None
		* create_time: None
  * update
	* Query Modifier:
	  * Set 0:
		* user: $__user
	* Doc Modifier:
	  * Set 0:
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
		* user: $__user
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
## Extended Attrs: None
## Cache Sets: None
## Analytics Sets: None