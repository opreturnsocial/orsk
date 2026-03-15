# ORK-04: Repost

**Kind Value:** `0x04` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

A pure repost of an existing ORS post. Contains only a reference to the original post's Bitcoin txid - no added content.

## Format

| Field             | Kind-data offset | Size     | Description                                           |
| ----------------- | ---------------- | -------- | ----------------------------------------------------- |
| `referenced_txid` | 0                | 32 bytes | txid of the post being reposted (internal byte order) |

**Kind data length:** exactly 32 bytes.

## Referenced Post

`referenced_txid` is the 32-byte txid in internal (little-endian) byte order - the same representation used in raw Bitcoin transaction serialization. To display or compare with explorer-style txids (big-endian hex), reverse the 32 bytes.

Parsers SHOULD verify the referenced post exists. Parsers MUST NOT reject a repost solely because the referenced post is unknown or not yet seen (e.g. out-of-order scanning).

## Validation

In addition to the base ORS-01 requirements:

1. Kind data MUST be exactly 32 bytes (no content field)
2. `referenced_txid` at kind-data bytes 0-31 MUST be 32 bytes
3. `referenced_txid` SHOULD reference a known ORS post

See [examples/ORK-04.md](examples/ORK-04.md) for encoding examples.
