# VBZS_JSONMove

```filemaker
VBZS_JSONMove ( json ; sourcePath ; targetPath )
```

Moves a JSON element from `sourcePath` to `targetPath`.

On a successful move, the source element is always removed.

## Source-path behavior

```text
INVALID_PATH   Return an error
NOT_FOUND      Return the original JSON unchanged
FOUND          Move if the target is valid
```

A valid path that does not exist is therefore not an error.

## Transactional behavior

The source is removed only after the target has been validated and the complete move can be performed.

If the target is invalid, the function returns an error result rather than partially modified JSON.

## Rename a key

Input:

```json
{
	"id": 123,
	"name": "Menno",
	"active": true
}
```

Call:

```filemaker
VBZS_JSONMove ( json ; "name" ; "customerName" )
```

Result:

```json
{
	"id": 123,
	"customerName": "Menno",
	"active": true
}
```

When a key is renamed within the same object and the destination does not yet exist, the new key retains the source key's position.

## Existing target key

If the target key already exists, its value is replaced at the target key's existing position. The source element is removed.

## Arrays

A numeric target index is an insertion position. Existing array members shift rather than being overwritten.

Input:

```json
{
	"items": ["A","B","C","D"]
}
```

Call:

```filemaker
VBZS_JSONMove ( json ; "items[1]" ; "items[3]" )
```

Result:

```json
{
	"items": ["A","C","D","B"]
}
```

Moving in the other direction:

```filemaker
VBZS_JSONMove ( json ; "items[3]" ; "items[1]" )
```

Result:

```json
{
	"items": ["A","D","B","C"]
}
```

## Append to an array

Use `[+]` as the final target path element:

```filemaker
VBZS_JSONMove (
    json ;
    "items[1]" ;
    "archive[+]"
)
```

The value is removed from `items` and appended to `archive`.

## Missing source

```filemaker
VBZS_JSONMove (
    "{\"id\":123,\"name\":\"Menno\"}" ;
    "missing" ;
    "other"
)
```

returns the original JSON unchanged.
