# ORK-03 Examples: Text Reply

Kind value: `0x03`. Kind-specific data (offset 101+) is a 32-byte `parent_txid` (internal byte order) followed by raw UTF-8 content.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Minimal Reply

Replying to a post with display txid `a1b2c3d4...` (big-endian hex). The `parent_txid` field stores the reversed (internal/LE) bytes.

```
Byte  100:      03                    kind = TEXT_REPLY
Bytes 101–132:  d4c3b2a1...           parent_txid (32 bytes, internal byte order)
Bytes 133+:     4e696365210a          raw UTF-8 content: "Nice!"
```

Full schematic:
```
4f525300 [PP×32] [SS×64] 03 [parent_txid×32] 4e69636521
```

- Sig covers: sha256(magic || version || pubkey || 0x03 || parent_txid_bytes || content_bytes)

## Example 2: Converting txid byte order

Explorer/display txid (big-endian hex, 32 bytes shown left-to-right):
```
a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90
```

Internal byte order (reverse the bytes for wire encoding):
```
908f7e6d5c4b3a291807f6e5d4c3b2a1908f7e6d5c4b3a291807f6e5d4c3b2a1
```

This reversed 32-byte sequence is what goes into `parent_txid` at offsets 101–132.

## Example 3: Unicode Reply

```
Byte  100:      03                    kind = TEXT_REPLY
Bytes 101–132:  <parent_txid, 32 bytes internal order>
Bytes 133+:     f09f9a80 20626974636f696e  UTF-8: "🚀 bitcoin"
```

## Test Vector: Valid Reply (schematic)

```
Header (101 bytes):
  4f525300            magic + version
  <pubkey: 32 bytes>  author x-only pubkey
  <sig: 64 bytes>     Schnorr sig of sha256(unsigned_payload)
  03                  kind = TEXT_REPLY

Kind-specific (offsets 101–132):
  <parent_txid: 32 bytes>   internal byte order (LE)

Content (offset 133+):
  476f6f6420706f737421      raw UTF-8: "Good post!"
```

Minimum valid payload: 134 bytes (101-byte header + 32 parent_txid + 1 content byte).
