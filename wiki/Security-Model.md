# Security Model

## Cryptography

- Encryption: AES-256-GCM
- Key derivation: Argon2id
  - Time cost: 4
  - Memory cost: 131072 KiB (128 MB)
  - Parallelism: 4
- Salt: 16 bytes per vault
- Nonce: 12 bytes per encryption

## Vault Storage

Vault file format:

```json
{
  "salt": "<base64>",
  "nonce": "<base64>",
  "data": "<base64>"
}
```

Default location: `~/.soteria/vault.json`

## Runtime Protections

- Auto-lock timeout
- Clipboard auto-clear
- Exponential unlock rate limiting
- Localhost-only IPC (`127.0.0.1:8722`)
- CORS origin validation for extension requests

## Threat Model Summary

Soteria protects strongly against offline vault theft and opportunistic local snooping.

Soteria does not protect against:

- A fully compromised operating system
- Malware with full user-level memory access
- Physical attacks on an unlocked machine
