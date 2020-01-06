[Back to Core Package Index](./README.md)

# Module: Session
`Session` module provides data type and controller for sessions in LIMP eco-system. CRUD methods of the module are supposed to used for internal calls only, while methods `auth`, `reauth`, and `signout` are available for use by API as well as internal calls when needed.
## Attrs
* user:
  * `_id` of `User` doc the doc belongs to.
  * Type: `<ATTR:ID,{}>`
* groups:
  * List of `_id` for every group the session is authenticated against. This attr is set by `auth` method when called with `groups` Doc Arg for Controller Auth Sequence.
  * Type: `<ATTR:LIST,{'list': [<ATTR:ID,{}>], 'min': None, 'max': None}>`
  * Default [groups]: []
* host_add:
  * IP of the host the user used to authenticate.
  * Type: `<ATTR:IP,{}>`
* user_agent:
  * User-agent of the app the user used to authenticate.
  * Type: `<ATTR:STR,{'pattern': None}>`
* expiry:
  * Python `datetime` ISO format of session expiry.
  * Type: `<ATTR:DATETIME,{'ranges': None}>`
* token:
  * System-generated session token.
  * Type: `<ATTR:STR,{'pattern': None}>`
* create_time:
  * Python `datetime` ISO format of the doc creation.
  * Type: `<ATTR:DATETIME,{'ranges': None}>`
## Methods
### Method: read
* Permissions Sets:
  * read
	* Query Modifier:
	  * Set 0:
		* user: $__user
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: create
* Permissions Sets:
  * create
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: update
* Permissions Sets:
  * update
	* Query Modifier:
	  * Set 0:
		* user: $__user
	* Doc Modifier:
	  * Set 0:
		* user: None
		* create_time: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
### Method: delete
* Permissions Sets:
  * delete
	* Query Modifier:
	  * Set 0:
		* user: $__user
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
### Method: auth
* Permissions Sets:
  * *
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: reauth
* Permissions Sets:
  * *
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>, 'hash': <ATTR:STR,{'pattern': None}>, 'groups': <ATTR:LIST,{'list': [<ATTR:ID,{}>], 'min': None, 'max': None}>}`
  * `{'_id': <ATTR:ID,{}>, 'hash': <ATTR:STR,{'pattern': None}>}`
* Doc Args Sets: None
### Method: signout
* Permissions Sets:
  * *
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets:
  * `{'_id': <ATTR:ID,{}>}`
* Doc Args Sets: None
## Extended Attrs
* user:
  * Module: 'user'
  * Extend Attrs: '['*']'
  * Force: 'True'
## Cache Sets: None
## Analytics Sets: None