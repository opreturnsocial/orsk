# ORK-05: Quote Repost

**Kind Value:** `0x05` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

A repost of an existing ORS post with added commentary. Extends ORK-04 with a UTF-8 content field beginning at kind-data offset 32.

## Format

| Field             | Kind-data offset | Size     | Description                                               |
| ----------------- | ---------------- | -------- | --------------------------------------------------------- |
| `referenced_txid` | 0                | 32 bytes | txid of the post being quoted (internal byte order)       |
| `content`         | 32               | variable | UTF-8 quote commentary                                    |

**Minimum kind data length:** 33 bytes.

## Referenced Post

`referenced_txid` is the 32-byte txid in internal (little-endian) byte order - the same representation used in raw Bitcoin transaction serialization. To display or compare with explorer-style txids (big-endian hex), reverse the 32 bytes.

Parsers SHOULD verify the referenced post exists. Parsers MUST NOT reject a quote repost solely because the referenced post is unknown or not yet seen (e.g. out-of-order scanning).

## Content

Content starts at kind-data offset 32.

## Validation

In addition to the base ORS-01 requirements:

1. Kind data MUST be at least 33 bytes
2. `referenced_txid` at kind-data bytes 0-31 MUST be 32 bytes
3. Content MUST be at least 1 byte
4. `referenced_txid` SHOULD reference a known ORS post

See [examples/ORK-05.md](examples/ORK-05.md) for encoding examples.
