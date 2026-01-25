# Soteria

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.9+-green.svg)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg)

A secure, local-first password manager with desktop GUI, CLI, and browser extension.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    User Interfaces                          │
├───────────────┬───────────────┬─────────────────────────────┤
│  Desktop GUI  │      CLI      │     Browser Extension       │
│  (Tkinter)    │   (argparse)  │   (Chrome/Edge/Brave)       │
└───────┬───────┴───────┬───────┴──────────────┬──────────────┘
        │               │                      │
        │               │          IPC (localhost:8722)
        │               │                      │
        ▼               ▼                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   Core Library (soteria/)                   │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐    │
│  │ vault.py │  │crypto.py │  │storage.py│  │models.py │    │
│  │   CRUD   │  │ AES-GCM  │  │ Atomic   │  │ Password │    │
│  │  Index   │  │ Argon2id │  │  Writes  │  │  Entry   │    │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘    │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
                 ~/.soteria/vault.json
                      (encrypted)
```

---

## Security Model

### Cryptographic Choices

| Component | Algorithm | Parameters |
|-----------|-----------|------------|
| Key Derivation | Argon2id | 4 iterations, 128 MB memory, 4 threads |
| Encryption | AES-256-GCM | 12-byte nonce, authenticated |
| Salt | Random | 16 bytes per vault |
| Entry IDs | UUID4 | Cryptographically random |

### Vault File Format

```json
{
  "salt": "<base64 16 bytes>",
  "nonce": "<base64 12 bytes>",
  "data": "<base64 encrypted JSON>"
}
```

### Runtime Protections

- **Auto-lock**: Configurable 1-30 minute timeout
- **Clipboard clear**: Configurable 15s-2min with secure overwrite
- **Rate limiting**: Exponential backoff after 5 failed unlock attempts
- **File permissions**: 0600 (Unix) for vault file
- **Password field auto-hide**: 10 second timeout

---

## IPC Server API

The desktop app exposes a localhost HTTP API for browser extension communication.

**Base URL:** `http://127.0.0.1:8722`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/vault/status` | POST | Check if vault is unlocked |
| `/api/vault/unlock` | POST | Unlock vault with password |
| `/api/vault/lock` | POST | Lock the vault |
| `/api/entries/search` | POST | Search entries by query/domain |
| `/api/entries/get` | POST | Get entry with password by ID |
| `/api/entries/add` | POST | Add new entry |

### Security Constraints

- Binds only to `127.0.0.1` (localhost)
- CORS validated for extension origins
- Passwords never cached in extension
- Extension cannot unlock vault independently

---

## Data Flow

### Encryption (Save)

```
Password Entry → JSON serialize → AES-256-GCM encrypt → Base64 encode → Write file
                                        ↑
                        Master Password → Argon2id → 256-bit key
```

### Decryption (Load)

```
Read file → Base64 decode → AES-256-GCM decrypt → JSON parse → Password Entry
                                  ↑
                  Master Password → Argon2id → 256-bit key
```

GCM authentication tag validates decryption - wrong password = `InvalidTag` exception.

---

## Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| cryptography | >=41.0.0 | AES-256-GCM encryption |
| argon2-cffi | >=23.1.0 | Argon2id key derivation |
| pyperclip | >=1.8.0 | Clipboard access (optional) |
| keyboard | >=0.13.5 | Global hotkey (optional) |
| pystray | >=0.19.0 | System tray (optional) |
| Pillow | >=9.0.0 | Tray icon rendering (optional) |

---

## Building & Testing

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run Tests

```bash
python test_soteria.py
```

### Build Executable (Windows)

```powershell
.\build.bat
```

Output: `dist\SoteriaApp\SoteriaApp.exe`

### Run Application

```bash
# GUI mode
python main.py --gui

# CLI mode
python main.py <command>

# Start minimized to tray
python main.py --gui --minimized
```

---

## Browser Extension

### Architecture

```
browser_extension/
├── manifest.json     # Manifest V3 config
├── background.js     # Service worker, IPC client
├── content.js        # Form detection, autofill
└── popup.html/js/css # Extension UI
```

### Installation

1. Open `chrome://extensions` (or `edge://extensions`)
2. Enable "Developer mode"
3. Click "Load unpacked"
4. Select the `browser_extension/` folder

### Permissions

- `activeTab`: Autofill on current page
- `clipboardWrite`: Copy passwords
- `tabs`: Get current domain
- `host_permissions`: `http://127.0.0.1:8722/*` for IPC

---

## Contributing

### Code Structure

```
soteria/
├── vault.py      # Vault class - all CRUD operations
├── crypto.py     # Encryption/decryption primitives
├── storage.py    # File I/O with atomic writes
├── models.py     # PasswordEntry dataclass
├── cli.py        # CLI argument handling
├── ipc_server.py # HTTP API for browser extension
└── gui/
    ├── app.py    # Main Tkinter application
    ├── styles.py # Color scheme and fonts
    ├── tray.py   # System tray integration
    ├── frames/   # Login and main vault frames
    ├── dialogs/  # Entry, generator, settings dialogs
    └── widgets/  # PasswordField, Toast components
```

### Input Validation Limits

| Field | Max Length |
|-------|------------|
| Service | 100 chars |
| Username | 255 chars |
| Password | 1024 chars |
| URL | 2048 chars |
| Notes | 10000 chars |

### Key Implementation Notes

1. Multiple entries per service allowed (different usernames)
2. Search is case-insensitive substring match
3. Entry IDs are UUID4, stable across lock/unlock
4. Master password change regenerates salt
5. Atomic file writes (temp file + rename)
6. O(1) entry lookup via ID and service indexes

---

## License

MIT License - See [LICENSE](LICENSE) for details.

---

**GitHub:** [github.com/nikokiru/soteria](https://github.com/nikokiru/soteria)
