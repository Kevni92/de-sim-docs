# Deutschland-Simulator – Dokumentation

Modulare Dokumentation für einen transparenten Staatshaushalts- und Wirkungssimulator.

- Öffentliche fachliche Dokumentation: https://kevni92.github.io/de-sim-docs/
- Fachlicher Einstieg: `docs/00-meta/index.md`
- Maschinenlesbarer Fachindex: `docs/llms.txt`
- Deployment: `.github/workflows/pages.yml`

## Veröffentlichungsumfang

Die GitHub Page veröffentlicht ausschließlich fachliche Inhalte:

- Staatshaushalt, Steuern und Leistungen,
- Bevölkerung und Haushalte,
- direkte und indirekte Wirkungsketten,
- Demografie, Bildung und Gesundheit,
- Evidenz, Quellen, Unsicherheiten und Neutralitätsregeln.

Interne Anforderungskataloge, Softwarearchitektur, Design-Prompts und Umsetzungsplanung bleiben im Repository erhalten, sind aber über `exclude_docs` von Build, Navigation und Suche der öffentlichen Seite ausgeschlossen.

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

Jeder Push auf `main` baut und veröffentlicht die fachliche Dokumentation über GitHub Actions.
