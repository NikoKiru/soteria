# Browser Extension

The Soteria extension supports Chrome, Edge, and Brave.

## Install (Unpacked)

1. Open your browser extension page:
   - Chrome: `chrome://extensions`
   - Edge: `edge://extensions`
   - Brave: `brave://extensions`
2. Enable Developer mode.
3. Click **Load unpacked**.
4. Select the `browser_extension` folder.

## Requirements

- Soteria desktop app must be running.
- Vault must be unlocked.
- IPC server is localhost-only (`127.0.0.1:8722`).

## What It Can Do

- Search entries
- Copy passwords
- Autofill detected login forms
- Lock the vault remotely

## What It Cannot Do

- Unlock the vault

## If Extension Shows Not Connected

- Start the desktop app
- Unlock the vault
- Reload the extension
