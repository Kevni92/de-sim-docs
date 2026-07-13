# Deutschland-Simulator – Dokumentation

Modulare Planungs- und Forschungsdokumentation für einen transparenten Staatshaushalts- und Wirkungssimulator.

- Dokumentation: https://kevni92.github.io/de-sim-docs/
- KI-Leseindex: `docs/00-meta/ki-leseindex.md`
- Deployment: `.github/workflows/pages.yml`

## Lokal starten

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

## Prüfen

```bash
mkdocs build --strict
```

Jeder Push auf `main` baut und veröffentlicht die Dokumentation über GitHub Actions.
