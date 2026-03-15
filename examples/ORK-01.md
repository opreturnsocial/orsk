# ORK-01 Examples: Text Note

Kind value: `0x01`. Kind-specific data is raw UTF-8 content.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Minimal Text Post

```
Kind byte:        01                                (kind = TEXT_NOTE)
Kind data byte 0+: 48656c6c6f20776f726c6421...      (raw UTF-8 content)
```

- Kind: `0x01` (TEXT_NOTE)
- Content (kind data byte 0): raw UTF-8 "Hello world! bitcoin social is here!"

## Example 2: Unicode Content

```
Content: "🚀 bitcoin 🧡"
Content bytes (UTF-8): f09f9a80 20626974636f696e20 f09fa4a1  (22 bytes)

Kind byte:        01              kind = TEXT_NOTE
Kind data byte 0+: f09f9a80...   raw UTF-8 content (22 bytes)
```

## Test Vector: Valid Text Post (schematic)

```
Kind byte:
  01                  kind = TEXT_NOTE

Kind-specific data:
  48656c6c6f20576f726c6421  raw UTF-8: "Hello World!"
```
