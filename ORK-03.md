# ORK-03: Text Reply

**Kind Value:** `0x03` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

A reply to an existing ORS post (any kind). Extends a TEXT_NOTE with a reference
to the parent post's Bitcoin txid.

## Format

| Field         | Offset | Size     | Description                                             |
| ------------- | ------ | -------- | ------------------------------------------------------- |
| `parent_txid` | 101    | 32 bytes | txid of the post being replied to (internal byte order) |
| `content`     | 133    | variable | UTF-8 reply text                                        |

**Minimum payload length:** 134 bytes.

## Parent Reference

`parent_txid` is the 32-byte txid of the parent post in internal (little-endian) byte order -
the same representation used in raw Bitcoin transaction serialization. To display or compare
with explorer-style txids (big-endian hex), reverse the 32 bytes.

Parsers SHOULD verify the referenced parent exists. Parsers MUST NOT reject a reply solely
because the parent is unknown or not yet seen (e.g. out-of-order scanning).

## Content

Content starts at offset 133.

## Validation

In addition to the base ORS-01 requirements:

1. Payload MUST be at least 134 bytes
2. `parent_txid` at offsets 101-132 MUST be 32 bytes
3. Content MUST be at least 1 byte
4. `parent_txid` SHOULD reference a known ORS post

See [examples/ORK-03.md](examples/ORK-03.md) for encoding examples.
