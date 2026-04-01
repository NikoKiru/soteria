# Development Guide

## Setup

```bash
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

## Test

```bash
python -m pytest tests/ -v
```

## Lint

```bash
ruff check soteria/
```

## Run App

```bash
python main.py --gui
python main.py init
```

## Build

```powershell
.\build.bat
.\build_headless.bat
```

## Deploy (Windows, Admin)

```powershell
.\deploy.ps1
```

## Release Checklist

1. Run tests and lint.
2. Validate GUI and extension workflows manually.
3. Build GUI and headless binaries.
4. Update docs and changelog/updates.
