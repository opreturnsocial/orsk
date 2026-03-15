# ORK-06 Examples: Follow

Kind value: `0x06`. Kind-specific data is a 32-byte `target_pubkey` (x-only Schnorr) followed by 1-byte `action`.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Follow

```
Kind byte:              06                    kind = FOLLOW
Kind data bytes 0-31:   <target_pubkey: 32 bytes>  x-only pubkey of the account to follow
Kind data byte 32:      01                    action = follow
```

## Example 2: Unfollow

```
Kind byte:              06                    kind = FOLLOW
Kind data bytes 0-31:   <target_pubkey: 32 bytes>  x-only pubkey of the account to unfollow
Kind data byte 32:      00                    action = unfollow
```

## Semantics: Latest Wins

Follow state for a (followerPubkey, targetPubkey) pair is resolved by the post with the highest block height. If two posts share the same block, the earlier transaction index wins.

## Validation Notes

- Kind data MUST be exactly 33 bytes
- `target_pubkey` at kind-data bytes 0-31 MUST be 32 valid bytes
- `action` at kind-data byte 32 MUST be `0x01` (follow) or `0x00` (unfollow)
- `target_pubkey` MUST NOT equal the author's `pubkey` (no self-follows)

## Test Vector: Valid Follow (schematic)

```
Kind byte:
  06                  kind = FOLLOW

Kind-specific data bytes 0-31:
  <target_pubkey: 32 bytes>   x-only pubkey to follow/unfollow

Kind-specific data byte 32:
  01                          action = follow (00 = unfollow)
```

Exact kind data length: 33 bytes.
