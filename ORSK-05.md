# ORSK-05: Quote Repost

**Kind Value:** `0x05` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

A repost of an existing ORS post with added commentary. Extends ORSK-04 with a UTF-8 content field beginning at offset 133.

## Format

| Field             | Offset | Size     | Description                                               |
| ----------------- | ------ | -------- | --------------------------------------------------------- |
| `referenced_txid` | 101    | 32 bytes | txid of the post being quoted (internal byte order)       |
| `content`         | 133    | variable | UTF-8 quote commentary                                    |

**Minimum payload length:** 134 bytes.

## Referenced Post

`referenced_txid` is the 32-byte txid in internal (little-endian) byte order - the same representation used in raw Bitcoin transaction serialization. To display or compare with explorer-style txids (big-endian hex), reverse the 32 bytes.

Parsers SHOULD verify the referenced post exists. Parsers MUST NOT reject a quote repost solely because the referenced post is unknown or not yet seen (e.g. out-of-order scanning).

## Content

Content starts at offset 133.

## Validation

In addition to the base ORS-01 requirements:

1. Payload MUST be at least 134 bytes
2. `referenced_txid` at offsets 101-132 MUST be 32 bytes
3. Content MUST be at least 1 byte
4. `referenced_txid` SHOULD reference a known ORS post

See [examples/ORSK-05.md](examples/ORSK-05.md) for encoding examples.
