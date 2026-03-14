# ORSK-02 Examples: Profile Update

Kind value: `0x02`. Kind-specific data (offset 101+) is a 1-byte propertyKind followed by the raw value.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Name

```
Byte  100:   02              kind = PROFILE_UPDATE
Byte  101:   00              propertyKind = name (0x00)
Bytes 102+:  416c696365      value = "Alice"
```

Full schematic:
```
4f525300 [PP×32] [SS×64] 02 00 416c696365
```

- Sig covers: sha256(magic || version || pubkey || 0x02 || 0x00 || "Alice")

## Example 2: Bot Flag

```
Byte  100:   02              kind = PROFILE_UPDATE
Byte  101:   04              propertyKind = bot (0x04)
Byte  102:   01              value = true (0x01 = true, 0x00 = false)
```

## Example 3: Avatar URL

```
Byte  100:   02              kind = PROFILE_UPDATE
Byte  101:   01              propertyKind = avatar_url (0x01)
Bytes 102+:  <UTF-8 URL bytes>
```
