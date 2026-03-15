# ORK-06 Examples: Follow

Kind value: `0x06`. Kind-specific data (offset 101+) is a 32-byte `target_pubkey` (x-only Schnorr) followed by 1-byte `action`.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Follow

```
Byte  100:      06                    kind = FOLLOW
Bytes 101–132:  <target_pubkey: 32 bytes>  x-only pubkey of the account to follow
Byte  133:      01                    action = follow
```

Full schematic:
```
4f525300 [PP×32] [SS×64] 06 [target_pubkey×32] 01
```

- Sig covers: sha256(magic || version || pubkey || 0x06 || target_pubkey || action)

## Example 2: Unfollow

```
Byte  100:      06                    kind = FOLLOW
Bytes 101–132:  <target_pubkey: 32 bytes>  x-only pubkey of the account to unfollow
Byte  133:      00                    action = unfollow
```

Full schematic:
```
4f525300 [PP×32] [SS×64] 06 [target_pubkey×32] 00
```

## Semantics: Latest Wins

Follow state for a (followerPubkey, targetPubkey) pair is resolved by the post with the highest block height. If two posts share the same block, the earlier transaction index wins.

## Validation Notes

- Payload MUST be exactly 134 bytes
- `target_pubkey` at offsets 101-132 MUST be 32 valid bytes
- `action` at offset 133 MUST be `0x01` (follow) or `0x00` (unfollow)
- `target_pubkey` MUST NOT equal the author's `pubkey` (no self-follows)

## Test Vector: Valid Follow (schematic)

```
Header (101 bytes):
  4f525300            magic + version
  <pubkey: 32 bytes>  author x-only pubkey
  <sig: 64 bytes>     Schnorr sig of sha256(unsigned_payload)
  06                  kind = FOLLOW

Kind-specific (offsets 101–133):
  <target_pubkey: 32 bytes>   x-only pubkey to follow/unfollow
  01                          action = follow (00 = unfollow)
```

Exact payload length: 134 bytes.
