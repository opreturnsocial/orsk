# ORS Kind Registry (ORSK)

This document defines the content kinds supported by the ORS protocol.

## Registry

| Kind Value | Name | Description | Spec |
|------------|------|-------------|------|
| `0x01` | TEXT_NOTE | Plain text post | [ORSK-01](ORSK-01.md) |
| `0x02` | PROFILE_UPDATE | Single profile field update | [ORSK-02](ORSK-02.md) |
| `0x03` | TEXT_REPLY | Reply to an existing ORS post | [ORSK-03](ORSK-03.md) |
| `0x04` | REPOST | Pure repost of an existing ORS post | [ORSK-04](ORSK-04.md) |
| `0x05` | QUOTE_REPOST | Repost with added commentary | [ORSK-05](ORSK-05.md) |
| `0x06` | FOLLOW | Follow or unfollow a pubkey | [ORSK-06](ORSK-06.md) |

## Reserved Values

| Range | Purpose |
|-------|---------|
| `0x00` | Reserved (never valid) |
| `0x01-0x7f` | Standard kinds (community defined) |
| `0x80-0xff` | Experimental / application-specific |

## Adding New Kinds

To propose a new kind:

1. Create an ORSK-XX spec document
2. Open a PR against this registry
3. Kind value is assigned sequentially
