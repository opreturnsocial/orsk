# ORK-01 Examples: Text Note

Kind value: `0x01`. Kind-specific data (offset 101+) is raw UTF-8 content.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Minimal Text Post

```
Bytes 0-3:   4f525300                          (magic + version)
Bytes 4-35:  <32-byte pubkey placeholder>
             aabbccdd...aabbccdd
Bytes 36-99: <64-byte sig placeholder>
             11223344...11223344
Byte  100:   01                                (kind = TEXT_NOTE)
Bytes 101+:  48656c6c6f20776f726c6421...        (raw UTF-8 content)
```

Full hex (schematic — `PP` = pubkey bytes, `SS` = sig bytes):
```
4f525300 [PP×32] [SS×64] 01 48656c6c6f20776f726c642120426974636f696e20736f6369616c206973206865726521
```

- Kind: `0x01` (TEXT_NOTE) at offset 100
- Content (offset 101): raw UTF-8 "Hello world! bitcoin social is here!"
- Sig covers: sha256(magic || version || pubkey || 0x01 || content_bytes)

## Example 2: Unicode Content

```
Content: "🚀 bitcoin 🧡"
Content bytes (UTF-8): f09f9a80 20626974636f696e20 f09fa4a1  (22 bytes)

Byte  100:   01              kind = TEXT_NOTE
Bytes 101+:  f09f9a80...     raw UTF-8 content (22 bytes)
```

## Test Vector: Valid Text Post (schematic)

```
Header (101 bytes):
  4f525300            magic + version
  <pubkey: 32 bytes>  author x-only pubkey
  <sig: 64 bytes>     Schnorr sig of sha256(unsigned_payload)
  01                  kind = TEXT_NOTE

Content (offset 101+):
  48656c6c6f20576f726c6421  raw UTF-8: "Hello World!"
```
