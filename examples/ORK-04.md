# ORK-04 Examples: Repost

Kind value: `0x04`. Kind-specific data (offset 101+) is a single 32-byte `referenced_txid` (internal byte order). No content field.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Basic Repost

Reposting a post with display txid `a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90` (big-endian hex). The `referenced_txid` field stores the reversed (internal/LE) bytes.

```
Byte  100:      04                    kind = REPOST
Bytes 101–132:  908f7e6d...b2a1       referenced_txid (32 bytes, internal byte order)
```

Full schematic:

```
4f525300 [PP×32] [SS×64] 04 [referenced_txid×32]
```

- Total payload: exactly 133 bytes
- Sig covers: sha256(magic || version || pubkey || 0x04 || referenced_txid_bytes)

## Example 2: Converting txid byte order

Explorer/display txid (big-endian hex, as shown in block explorers):

```
a1b2c3d4e5f60718293a4b5c6d7e8f90a1b2c3d4e5f60718293a4b5c6d7e8f90
```

Internal byte order (reverse the bytes for wire encoding):

```
908f7e6d5c4b3a291807f6e5d4c3b2a1908f7e6d5c4b3a291807f6e5d4c3b2a1
```

This reversed 32-byte sequence is what goes into `referenced_txid` at offsets 101–132.

## Test Vector: Valid Repost (schematic)

```
Header (101 bytes):
  4f525300            magic + version
  <pubkey: 32 bytes>  author x-only pubkey
  <sig: 64 bytes>     Schnorr sig of sha256(unsigned_payload)
  04                  kind = REPOST

Kind-specific (offsets 101–132):
  <referenced_txid: 32 bytes>   internal byte order (LE)
```

Exact valid payload: 133 bytes (101-byte header + 32 referenced_txid bytes).
