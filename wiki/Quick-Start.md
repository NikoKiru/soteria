# Quick Start

## 1. Install Dependencies

```bash
pip install -r requirements.txt
```

Optional for development:

```bash
pip install -r requirements-dev.txt
```

## 2. Create a Vault

```bash
python main.py init
```

## 3. Add an Entry

```bash
python main.py add github myuser --generate --length 24
```

## 4. Retrieve an Entry

```bash
python main.py get github --clip
```

## 5. Launch GUI

```bash
python main.py --gui
```

## 6. Optional: Start Minimized

```bash
python main.py --gui --minimized
```

## Vault Location

Soteria stores your encrypted vault at:

- `~/.soteria/vault.json`
