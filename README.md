# VBZS_JSON

VBZS_JSON is a FileMaker plug-in with additional functions for creating, modifying, merging, moving, formatting, and displaying JSON.

A key design goal is to preserve the original order of JSON object keys. This makes VBZS_JSON useful where FileMaker's built-in JSON functions change the key order or make order-preserving changes difficult.

## Functions

- [VBZS_JSONAddElement](docs/VBZS_JSONAddElement.md)
- [VBZS_JSONColoring](docs/VBZS_JSONColoring.md)
- [VBZS_JSONDelete](docs/VBZS_JSONDelete.md)
- [VBZS_JSONLicenseInfo](docs/VBZS_JSONLicenseInfo.md)
- [VBZS_JSONMerge](docs/VBZS_JSONMerge.md)
- [VBZS_JSONMove](docs/VBZS_JSONMove.md)
- [VBZS_JSONPrettyPrint](docs/VBZS_JSONPrettyPrint.md)
- [VBZS_JSONRegister](docs/VBZS_JSONRegister.md)

The plug-in also provides version and licensing functions. Registration documentation can be copied from the VBZS plug-in and adapted to the VBZS_JSON function names and license identity.

## Design principles

VBZS_JSON does not attempt to replace FileMaker's built-in JSON functionality. It adds operations that are difficult or unpredictable with the standard functions, particularly when object-key order must be preserved.

The first release provides six JSON functions:

```text
AddElement
Coloring
Delete
Merge
Move
PrettyPrint
```

Together they allow JSON to be deleted, formatted, merged, extended, colored, and moved while avoiding unnecessary changes to object order.

## Object order

VBZS_JSON uses order-preserving JSON processing for functions that parse and rebuild JSON.

General rules are:

- Existing object keys stay at their existing position whenever possible.
- New object keys are appended in the order in which they are supplied.
- Updating an existing key changes its value without moving the key.
- Array order is preserved unless a function explicitly inserts, appends, deletes, or moves an array element.

## Function naming

Functions follow FileMaker's JSON naming convention with the `VBZS_` prefix identifying the plug-in origin, for example:

```text
JSONSetElement         FileMaker
VBZS_JSONAddElement    VBZS_JSON

JSONFormatElements     FileMaker
VBZS_JSONPrettyPrint   VBZS_JSON
```

## Licensing

VBZS_JSON has its own license identity. A VBZS license does not register VBZS_JSON and a VBZS_JSON license does not register VBZS.

The two plug-ins can be loaded at the same time.
