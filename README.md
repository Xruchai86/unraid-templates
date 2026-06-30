# Unraid Templates

Sammlung sauberer Unraid-Community-Apps-Templates für meine selbst gehosteten Container.
**Enthält bewusst keine echten Netzwerk-/System-Daten** – alle Werte sind generische Beispiele oder leere Platzhalter, die beim Installieren gesetzt werden.

## Struktur
- `templates/` – ein `<app>.xml` pro Container.
- `templates/_skeleton.xml` – Vorlage zum Kopieren für neue Apps.
- `.github/workflows/build.yml` – universeller Workflow; gehört in **jedes App-Code-Repo** (nicht hierher), baut & pusht das Image nach `ghcr.io/<owner>/<repo>`.

## Image bauen (pro App)
1. App-Code-Repo mit `Dockerfile`.
2. `build.yml` ins App-Repo unter `.github/workflows/` kopieren.
3. Push auf `main` (oder Tag `v1.0.0`) → Image landet unter `ghcr.io/<owner>/<repo>:latest`.
4. Package-Sichtbarkeit auf GitHub setzen: **public** (frei ziehbar) oder **private** (nur eingeladene Personen, siehe unten).

## Verteilung
**Öffentlich (Community Apps Store):** Dieses Repo über das Submission-Portal `ca.unraid.net` einreichen (XML-Format/Feld-Referenz dort dokumentiert).

**Nur für Eingeladene – Variante A (einfach):** Image *public* lassen, dieses Repo *nicht* einreichen. Freunde tragen die Repo-URL in Unraid unter **Docker → „Template repositories"** ein → **Add Container** → Template wählen. Nur wer die URL kennt, findet es.

**Nur für Eingeladene – Variante B (echter Zugriffsschutz):** Image *private* auf GHCR, gezielt Personen als Package-Collaborator einladen. Jede:r legt einen PAT mit `read:packages` an und hinterlegt die GHCR-Credentials in den Unraid-Docker-Einstellungen. Template-Repo darf trotzdem public sein – die Kontrolle sitzt am Image.

> Hinweis: Jedes App-**Code**-Repo separat ebenfalls von echten Default-Werten säubern (Hostnamen, IPs, Keys), damit das gebaute Image sauber ist.
