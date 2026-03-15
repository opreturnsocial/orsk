# ORK-06: Follow

**Kind Value:** `0x06` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

Declares a follow or unfollow of another pubkey. "Latest published wins" per (follower pubkey, target pubkey) pair.

## Format

| Field           | Offset | Size     | Description                                      |
| --------------- | ------ | -------- | ------------------------------------------------ |
| `target_pubkey` | 101    | 32 bytes | x-only Schnorr pubkey of the account to follow   |
| `action`        | 133    | 1 byte   | `0x01` = follow, `0x00` = unfollow               |

**Exact payload length:** 134 bytes.

## Semantics

Follow state for a given (followerPubkey, targetPubkey) pair is resolved by the post with the highest block height. If two posts share the same block, the earlier transaction index wins.

A pubkey MUST NOT follow itself. Parsers SHOULD ignore self-follow payloads.

## Validation

In addition to the base ORS-01 requirements:

1. Payload MUST be exactly 134 bytes
2. `target_pubkey` at offsets 101-132 MUST be 32 bytes
3. `action` at offset 133 MUST be `0x01` or `0x00`
4. `target_pubkey` MUST NOT equal the author's `pubkey`

See [examples/ORK-06.md](examples/ORK-06.md) for encoding examples.
