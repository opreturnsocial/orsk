# ORK-06: Follow

**Kind Value:** `0x06` | **Base Protocol:** [ORS-01](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md)

Declares a follow or unfollow of another pubkey. "Latest published wins" per (follower pubkey, target pubkey) pair.

## Format

| Field           | Kind-data offset | Size     | Description                                      |
| --------------- | ---------------- | -------- | ------------------------------------------------ |
| `target_pubkey` | 0                | 32 bytes | x-only Schnorr pubkey of the account to follow   |
| `action`        | 32               | 1 byte   | `0x01` = follow, `0x00` = unfollow               |

**Kind data length:** exactly 33 bytes.

## Semantics

Follow state for a given (followerPubkey, targetPubkey) pair is resolved by the post with the highest block height. If two posts share the same block, the earlier transaction index wins.

A pubkey MUST NOT follow itself. Parsers SHOULD ignore self-follow payloads.

## Validation

In addition to the base ORS-01 requirements:

1. Kind data MUST be exactly 33 bytes
2. `target_pubkey` at kind-data bytes 0-31 MUST be 32 bytes
3. `action` at kind-data byte 32 MUST be `0x01` or `0x00`
4. `target_pubkey` MUST NOT equal the author's `pubkey`

See [examples/ORK-06.md](examples/ORK-06.md) for encoding examples.
