# SENGA‑OPS Documentation

This repository hosts the public docs for **SENGA‑OPS** (SENGA+ with the **OPS** DSL). The site is built with Sphinx and published on Read the Docs.

## Edit locally

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
sphinx-build -b html source build/html
python -m http.server --directory build/html 8000
```

## Publish

Push to `main`. Read the Docs will build automatically using `.readthedocs.yaml`.
