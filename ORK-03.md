# ORK-03: Text Reply

**Kind Value:** `0x03` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

A reply to an existing ORS transaction (any kind). Extends a TEXT_NOTE with a reference
to the parent ORS transaction's Bitcoin txid.

## Format

| Field         | Kind-data offset | Size     | Description                                             |
| ------------- | ---------------- | -------- | ------------------------------------------------------- |
| `parent_txid` | 0                | 32 bytes | txid of the ORS transaction being replied to (internal byte order) |
| `content`     | 32               | variable | UTF-8 reply text                                        |

**Minimum kind data length:** 33 bytes.

## Parent Reference

`parent_txid` is the 32-byte txid of the parent post in internal (little-endian) byte order -
the same representation used in raw Bitcoin transaction serialization. To display or compare
with explorer-style txids (big-endian hex), reverse the 32 bytes.

Parsers SHOULD verify the referenced parent exists. Parsers MUST NOT reject a reply solely
because the parent is unknown or not yet seen (e.g. out-of-order scanning).

## Content

Content starts at kind-data offset 32.

## Validation

In addition to the base ORS-01 requirements:

1. Kind data MUST be at least 33 bytes
2. `parent_txid` at kind-data bytes 0-31 MUST be 32 bytes
3. Content MUST be at least 1 byte
4. `parent_txid` SHOULD reference a known ORS transaction

See [examples/ORK-03.md](examples/ORK-03.md) for encoding examples.
