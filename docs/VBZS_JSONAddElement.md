# VBZS_JSONAddElement

```filemaker
VBZS_JSONAddElement ( json ; path ; value ; type { ; path ; value ; type ; ... } )
```

Adds or updates one or more JSON elements while preserving existing object-key order.

Unlike FileMaker's `JSONSetElement`, multiple elements are supplied as consecutive groups of three parameters. The bracket grouping syntax used by FileMaker's built-in function is not available to external plug-in functions.

## Parameters

Each element consists of:

```text
path ; value ; type
```

Valid total parameter counts are therefore:

```text
4, 7, 10, 13, 16, ...
```

### JSON types

```text
JSONRaw       0
JSONString    1
JSONNumber    2
JSONObject    3
JSONArray     4
JSONBoolean   5
JSONNull      6
```

The type is required and may not be empty.

## Add one element

```filemaker
VBZS_JSONAddElement (
    "{}" ;
    "name" ;
    "Menno" ;
    JSONString
)
```

Result:

```json
{"name":"Menno"}
```

## Add multiple elements

```filemaker
VBZS_JSONAddElement (
    "{}" ;
    "name" ; "Menno" ; JSONString ;
    "age" ; 62 ; JSONNumber ;
    "active" ; True ; JSONBoolean
)
```

Result:

```json
{"name":"Menno","age":62,"active":true}
```

New keys are added in the order in which they are supplied.

## Updating an existing key

If the path already exists, only its value is changed. The key is not moved.

Input:

```json
{
	"name": "Menno",
	"age": 61,
	"active": true
}
```

Call:

```filemaker
VBZS_JSONAddElement ( json ; "age" ; 62 ; JSONNumber )
```

Result:

```json
{
	"name": "Menno",
	"age": 62,
	"active": true
}
```

## Arrays

### `[+]`

`[+]` appends a new array element and selects that new element.

### `[:]`

`[:]` refers to the element most recently added with `[+]` for that array.

Example:

```filemaker
VBZS_JSONAddElement (
    "{}" ;
    "people[+].name" ; "Menno" ; JSONString ;
    "people[:].age" ; 62 ; JSONNumber ;
    "people[:].city" ; "Woerden" ; JSONString ;
    "people[+].name" ; "Piet" ; JSONString ;
    "people[:].age" ; 55 ; JSONNumber
)
```

Result:

```json
{
	"people": [
		{
			"name": "Menno",
			"age": 62,
			"city": "Woerden"
		},
		{
			"name": "Piet",
			"age": 55
		}
	]
}
```

## Validation

The function stops at the first detected error and returns a readable message.

Validated conditions include:

- the total parameter count must be `3n + 1`;
- `path` must contain a text value and may not be empty;
- `type` is required;
- `type` must be `JSONRaw` through `JSONNull`, or numeric value `0` through `6`;
- JSON paths must be valid;
- input JSON must be valid.

Examples:

```text
? Invalid parameter count: received 6 parameters; 1 parameter is missing to complete the last path ; value ; type set.
```

```text
? Invalid path at element 2: path must contain a text value. Received: 62
```

```text
? Invalid JSON type at element 1: type is required (JSONRaw...JSONNull or 0...6).
```
