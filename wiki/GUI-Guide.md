# GUI Guide

## Launch

```bash
python main.py --gui
```

## Main Workflows

1. Unlock the vault with your master password.
2. Add entries from the main screen.
3. Search by service, username, or URL.
4. Copy passwords (clipboard clears automatically).
5. Lock the vault when done.

## Keyboard Shortcuts

- `Ctrl+N`: Add entry
- `Ctrl+F`: Focus search
- `Ctrl+L`: Lock vault
- `Ctrl+G`: Open generator
- `Ctrl+Q`: Quit app

## Security UX in GUI

- Auto-lock timeout is configurable (1-30 minutes)
- Clipboard clear timeout is configurable (15s-2m)
- Password fields auto-hide after a short delay
- Optional tray integration
