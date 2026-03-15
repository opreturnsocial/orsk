# ORK-02 Examples: Profile Update

Kind value: `0x02`. Kind-specific data is a 1-byte propertyKind followed by the raw value.

See [ORS-01.md](https://github.com/opreturnsocial/ors/blob/master/ORS-01.md) for the base header layout.

## Example 1: Name

```
Kind byte:          02              kind = PROFILE_UPDATE
Kind data byte 0:   00              propertyKind = name (0x00)
Kind data byte 1+:  416c696365      value = "Alice"
```

## Example 2: Bot Flag

```
Kind byte:          02              kind = PROFILE_UPDATE
Kind data byte 0:   04              propertyKind = bot (0x04)
Kind data byte 1:   01              value = true (0x01 = true, 0x00 = false)
```

## Example 3: Avatar URL

```
Kind byte:          02              kind = PROFILE_UPDATE
Kind data byte 0:   01              propertyKind = avatar_url (0x01)
Kind data byte 1+:  <UTF-8 URL bytes>
```
