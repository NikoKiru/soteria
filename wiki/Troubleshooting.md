# Troubleshooting

## Unlock Fails Repeatedly

- Verify the master password.
- Check for Caps Lock.
- Too many failed attempts trigger temporary lockout.

## Browser Extension Cannot Connect

- Ensure desktop app is running.
- Ensure vault is unlocked.
- Confirm localhost port `8722` is not blocked by security software.

## Autofill Does Not Work On A Site

- Some pages use custom forms and block autofill.
- Use search + copy as fallback.
- Refresh page and try again.

## Build Issues

Run:

```bash
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

Then:

```bash
python -m pytest tests/ -v
ruff check soteria/
```

## GUI Does Not Open

- Confirm Python and dependencies are installed.
- Run from project root.
- Try CLI to verify environment health:

```bash
python main.py list
```
