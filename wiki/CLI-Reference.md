# CLI Reference

## Core Commands

```bash
python main.py init
python main.py add <service> <username>
python main.py get <service>
python main.py list
python main.py delete <service>
python main.py search <query>
python main.py update <service>
python main.py change-master
python main.py generate
```

## Common Options

### add

- `--generate`
- `--length <n>`
- `--url <url>`
- `--notes <text>`

### get

- `--username <username>`
- `--clip`

### delete

- `--username <username>`
- `--force`

### update

- `--username <username>`
- `--new-username <username>`
- `--new-password <password>`
- `--new-url <url>`
- `--new-notes <text>`

### generate

- `--length <n>`
- `--clip`
- `--include-ambiguous`

## Examples

```bash
python main.py add github me@example.com --generate --length 32
python main.py get github --username me@example.com --clip
python main.py search git
python main.py update github --username me@example.com --new-url https://github.com
python main.py delete github --username me@example.com --force
```
