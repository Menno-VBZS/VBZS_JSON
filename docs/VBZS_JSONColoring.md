# VBZS_JSONColoring

```filemaker
VBZS_JSONColoring ( json { ; name ; color } )
```

Applies FileMaker text coloring to JSON without altering the original JSON text.

Object order, whitespace, indentation, Unicode text, diacritics, and emoji remain unchanged.

## Default coloring

```filemaker
VBZS_JSONColoring ( json )
```

uses:

```text
Object keys                 Blue
String values               Brown
Numbers, booleans and null  Black
```

## Highlighting selected properties

Supply `name` and `color` together:

```filemaker
VBZS_JSONColoring (
    json ;
    "comment" ;
    RGB ( 204 ; 0 ; 0 )
)
```

Matching is case-insensitive.

### Name matching

```text
comment       Exact match
*comment      Ends with comment
comment*      Starts with comment
*comment*     Contains comment
```

An asterisk has wildcard meaning only when it is the first and/or last character of `name`.

An asterisk elsewhere is interpreted literally:

```text
my*comment
```

matches the literal key `my*comment`.

## Colored property

When a key matches, the selected color is applied to the property and its complete value. The value may be a string, scalar, object, or array.

## Examples

Given:

```json
{
	"comment": "Exact",
	"apiComment": "Ends with comment",
	"commentText": "Starts with comment",
	"name": "Menno",
	"age": 62
}
```

```filemaker
VBZS_JSONColoring ( json ; "comment" ; RGB ( 204 ; 0 ; 0 ) )
```

highlights only `comment`.

```filemaker
VBZS_JSONColoring ( json ; "*comment" ; RGB ( 204 ; 0 ; 0 ) )
```

highlights keys ending in `comment`, including `comment` itself.
