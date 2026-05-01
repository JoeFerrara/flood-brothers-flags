# flood-brothers-flags

Public companion repo for [flood-brothers](https://github.com/JoeFerrara/flood-brothers).
Holds a single `flags.json` document the app fetches at launch and on each
foreground transition to decide which features are exposed.

This repo is intentionally tiny: no source code, no secrets, just the flag
document. The values inside are not PII — `allowListSHA256` is a list of
SHA-256 hex digests of `UIDevice.identifierForVendor` UUIDs. The raw UUID
never leaves the device.

## Schema

```json
{
  "notifications": {
    "global": false,
    "allowListSHA256": ["<sha256-hex-digest>"]
  }
}
```

- `global`: when `true`, the feature is on for everyone regardless of allow-list.
- `allowListSHA256`: SHA-256 hex digests; users whose hashed user ID matches
  any entry get the feature even when `global` is `false`.

## Editing

Push a commit to `main` with the desired changes. The app refetches on its
next launch / foreground transition (no app update required).
