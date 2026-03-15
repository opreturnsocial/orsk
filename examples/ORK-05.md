# ORK-05 Examples: Quote Repost

Kind value: `0x05`. Kind-specific data is a 32-byte `referenced_txid` (internal byte order) followed by raw UTF-8 content.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Basic Quote Repost

Quoting a post with display txid `a1b2c3d4...` (big-endian hex). The `referenced_txid` field stores the reversed (internal/LE) bytes.

```
Kind byte:              05                    kind = QUOTE_REPOST
Kind data bytes 0-31:   d4c3b2a1...           referenced_txid (32 bytes, internal byte order)
Kind data byte 32+:     5468697320697320677265617421  raw UTF-8: "This is great!"
```

## Example 2: Unicode Commentary

```
Kind byte:              05                    kind = QUOTE_REPOST
Kind data bytes 0-31:   <referenced_txid, 32 bytes internal order>
Kind data byte 32+:     f09f9a80 20626974636f696e  UTF-8: "🚀 bitcoin"
```

## Example 3: Converting txid byte order

Explorer/display txid (big-endian hex, as shown in block explorers):
```
a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90
```

Internal byte order (reverse the bytes for wire encoding):
```
908f7e6d5c4b3a291807f6e5d4c3b2a1908f7e6d5c4b3a291807f6e5d4c3b2a1
```

This reversed 32-byte sequence is what goes into `referenced_txid` at kind-data bytes 0-31.

## Test Vector: Valid Quote Repost (schematic)

```
Kind byte:
  05                  kind = QUOTE_REPOST

Kind-specific data bytes 0-31:
  <referenced_txid: 32 bytes>   internal byte order (LE)

Kind-specific data byte 32+:
  4c6f76652069742100            raw UTF-8: "Love it!"
```

Minimum valid kind data: 33 bytes (32 referenced_txid bytes + 1 content byte).
