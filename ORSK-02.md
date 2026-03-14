# ORSK-02: Profile Update

**Kind Value:** `0x02` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

Updates a single profile field for the author's pubkey. "Latest published wins" per pubkey+propertyKind.

## Kind-Specific Layout (offset 101+)

| Offset | Size | Description |
|--------|------|-------------|
| 101 | 1 | propertyKind byte |
| 102-end | variable | Raw value bytes |

## Property Kind Values

| Value | Name | Encoding |
|-------|------|----------|
| `0x00` | `name` | UTF-8 string |
| `0x01` | `avatar_url` | UTF-8 string (URL) |
| `0x02` | `bio` | UTF-8 string |
| `0x03` | `banner_url` | UTF-8 string (URL) |
| `0x04` | `bot` | 1 byte: `0x01`=true, `0x00`=false |
| `0x05` | `website_url` | UTF-8 string (URL) |

See [examples/ORSK-02.md](examples/ORSK-02.md) for encoding examples.

## Semantics

Profile state for a given pubkey+propertyKind is resolved by the post with the highest block height. If two posts share the same block, the earlier transaction index wins.

The `bot` field is normalised by parsers: `0x01` → `"true"`, `0x00` → `"false"`.

## Validation

Invalid if payload is shorter than 102 bytes (missing propertyKind byte).
