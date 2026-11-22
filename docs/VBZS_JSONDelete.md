# VBZS_JSONDelete

```filemaker
VBZS_JSONDelete ( json ; siblings ; keyOrIndexOrPath { ; keyOrIndexOrPath ; ... } )
```

Deletes one or more elements from JSON data while preserving the order of the remaining JSON.

## Parameters

### `json`

The JSON data to process.

### `siblings`

Controls wildcard behavior:

```text
False or empty   Delete only the first complete wildcard match
True             Delete all complete wildcard matches
```

This parameter has no effect on paths without a wildcard.

### `keyOrIndexOrPath`

One or more JSON paths identifying elements to delete.

Supported complete-element wildcards:

```text
*       object-name wildcard
[*]     array-index wildcard
```

Wildcards apply only at the specified level and are not recursive.

All paths are validated before any element is deleted. If the JSON or a supplied path is invalid, no deletion is performed.

## Examples

```filemaker
VBZS_JSONDelete ( json ; False ; "customers[1].name" )
```

Deletes only the explicitly specified element.

```filemaker
VBZS_JSONDelete ( json ; False ; "customers[*].password" )
```

Deletes the first complete match using the original JSON order.

```filemaker
VBZS_JSONDelete (
    json ;
    True ;
    "customers[*].password" ;
    "customers[*].internalId"
)
```

Deletes all matching `password` and `internalId` elements.
