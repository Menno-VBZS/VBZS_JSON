# VBZS_JSONPrettyPrint

```filemaker
VBZS_JSONPrettyPrint ( json )
```

Formats JSON as readable text without changing the original order of object keys.

This is the main difference from FileMaker's `JSONFormatElements` when key order must remain unchanged.

## Example

Input:

```json
{"z":1,"name":"Menno","address":{"country":"NL","city":"Woerden"},"a":2}
```

Result:

```json
{
	"z": 1,
	"name": "Menno",
	"address": {
		"country": "NL",
		"city": "Woerden"
	},
	"a": 2
}
```

The order remains:

```text
z
name
address
    country
    city
a
```

VBZS_JSONPrettyPrint uses one tab character per indentation level.

## Invalid JSON

Invalid JSON returns a readable error result:

```text
? Invalid JSON
```
