# VBZS_JSONMerge

```filemaker
VBZS_JSONMerge ( json1 ; json2 )
```

Merges two JSON values while preserving existing object-key order.

## Merge rules

```text
object + object   Merge recursively
array  + array    Append elements from json2
other cases       json2 replaces json1
```

### Objects

Objects are merged recursively.

Existing keys retain their position. New keys are appended in the order in which they occur in `json2`.

Example:

`json1`:

```json
{
	"name": "Menno",
	"address": {
		"city": "Woerden",
		"country": "NL"
	}
}
```

`json2`:

```json
{
	"address": {
		"city": "Utrecht",
		"street": "Voorbeeldstraat"
	},
	"active": true
}
```

Result:

```json
{
	"name": "Menno",
	"address": {
		"city": "Utrecht",
		"country": "NL",
		"street": "Voorbeeldstraat"
	},
	"active": true
}
```

`city` stays at its existing position while its value changes. `street` is appended.

### Arrays

When both values are arrays, the elements from `json2` are appended to `json1`.

```json
["A","B"]
```

plus:

```json
["C","D"]
```

becomes:

```json
["A","B","C","D"]
```

Array elements are not deduplicated or recursively merged with one another.

### Different value types

For scalar values or conflicting JSON types, the value from `json2` replaces the value from `json1`.

## Invalid JSON

Invalid input returns:

```text
? Invalid JSON
```
