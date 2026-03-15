# ORK-04 Examples: Repost

Kind value: `0x04`. Kind-specific data is a single 32-byte `referenced_txid` (internal byte order). No content field.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Basic Repost

Reposting a post with display txid `a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90` (big-endian hex). The `referenced_txid` field stores the reversed (internal/LE) bytes.

```
Kind byte:              04                    kind = REPOST
Kind data bytes 0-31:   908f7e6d...b2a1       referenced_txid (32 bytes, internal byte order)
```

- Kind data: exactly 32 bytes

## Example 2: Converting txid byte order

Explorer/display txid (big-endian hex, as shown in block explorers):

```
a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90
```

Internal byte order (reverse the bytes for wire encoding):

```
908f7e6d5c4b3a291807f6e5d4c3b2a1908f7e6d5c4b3a291807f6e5d4c3b2a1
```

This reversed 32-byte sequence is what goes into `referenced_txid` at kind-data bytes 0-31.

## Test Vector: Valid Repost (schematic)

```
Kind byte:
  04                  kind = REPOST

Kind-specific data bytes 0-31:
  <referenced_txid: 32 bytes>   internal byte order (LE)
```

Exact valid kind data: 32 bytes.
