# ORK-03 Examples: Text Reply

Kind value: `0x03`. Kind-specific data is a 32-byte `parent_txid` (internal byte order) followed by raw UTF-8 content.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Minimal Reply

Replying to a post with display txid `a1b2c3d4...` (big-endian hex). The `parent_txid` field stores the reversed (internal/LE) bytes.

```
Kind byte:              03                    kind = TEXT_REPLY
Kind data bytes 0-31:   d4c3b2a1...           parent_txid (32 bytes, internal byte order)
Kind data byte 32+:     4e696365210a          raw UTF-8 content: "Nice!"
```

## Example 2: Converting txid byte order

Explorer/display txid (big-endian hex, 32 bytes shown left-to-right):
```
a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90
```

Internal byte order (reverse the bytes for wire encoding):
```
908f7e6d5c4b3a291807f6e5d4c3b2a1908f7e6d5c4b3a291807f6e5d4c3b2a1
```

This reversed 32-byte sequence is what goes into `parent_txid` at kind-data bytes 0-31.

## Example 3: Unicode Reply

```
Kind byte:              03                    kind = TEXT_REPLY
Kind data bytes 0-31:   <parent_txid, 32 bytes internal order>
Kind data byte 32+:     f09f9a80 20626974636f696e  UTF-8: "🚀 bitcoin"
```

## Test Vector: Valid Reply (schematic)

```
Kind byte:
  03                  kind = TEXT_REPLY

Kind-specific data bytes 0-31:
  <parent_txid: 32 bytes>   internal byte order (LE)

Kind-specific data byte 32+:
  476f6f6420706f737421      raw UTF-8: "Good post!"
```

Minimum valid kind data: 33 bytes (32 parent_txid + 1 content byte).
