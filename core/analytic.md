[Back to Core Package Index](./README.md)

# Module: Analytic
`Analytic` module provides data type and controller from `Analytics Workflow` and accompanying analytics docs. It uses `pre_create` handler to assure no events duplications occur and all occurrences of the same event are recorded in one doc.
## Attrs
* user:
  * `_id` of `User` doc the doc belongs to.
  * Type: `<ATTR:ID,{}>`
* event:
  * Analytics event name.
  * Type: `<ATTR:STR,{'pattern': None}>`
* subevent:
  * Analytics subevent distinguishing attribute. This is usually `STR`, or `ID` but it is introduced in the module as `ANY` to allow wider use-cases by developers.
  * Type: `<ATTR:ANY,{}>`
* occurrences:
  * All occurrences of the event as list.
  * Type: `<ATTR:LIST,{'list': [<ATTR:DICT,{'dict': {'args': <ATTR:DICT,{'dict': {'__key': <ATTR:STR,{'pattern': None}>, '__val': <ATTR:ANY,{}>}}>, 'score': <ATTR:INT,{'range': None}>, 'create_time': <ATTR:DATETIME,{'ranges': None}>}}>], 'min': None, 'max': None}>`
* score:
  * Total score of all scores of all occurrences of the event. This can be used for data analysis.
  * Type: `<ATTR:INT,{'range': None}>`
## Methods
### Method: read
* Permissions Sets:
  * read
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: create
* Permissions Sets:
  * __sys
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* DOC Args Sets:
  * `{'event': <ATTR:STR,{'pattern': None}>, 'subevent': <ATTR:ANY,{}>, 'args': <ATTR:DICT,{'dict': {'__key': <ATTR:STR,{'pattern': None}>, '__val': <ATTR:ANY,{}>}}>}`
### Method: update
* Permissions Sets:
  * __sys
	* Query Modifier: None
	* Doc Modifier:
	  * Set 0:
		* user: None
		* create_time: None
* Query Args Sets: None
* Doc Args Sets: None
### Method: delete
* Permissions Sets:
  * delete
	* Query Modifier: None
	* Doc Modifier: None
* Query Args Sets: None
* Doc Args Sets: None
## Extended Attrs: None
## Cache Sets: None
## Analytics Sets: None