# LB 324

## Aufgabe 2

### Pre-commit installieren und einrichten

Zuerst muss `pre-commit` installiert werden:

```bash
py -m pip install pre-commit
```

Danach werden die beiden Git-Hooks installiert:

```bash
py -m pre_commit install
py -m pre_commit install -t pre-push
```

Die Konfiguration befindet sich in der Datei `.pre-commit-config.yaml`.

Beim Commit wird automatisch **Black** ausgeführt und der Python-Code formatiert.

Beim Push wird automatisch **pytest** ausgeführt und die vorhandenen Tests werden gestartet.

Die Konfiguration kann zusätzlich manuell überprüft werden:

```bash
py -m pre_commit validate-config
```

Die Commit-Hooks können manuell für alle Dateien ausgeführt werden:

```bash
py -m pre_commit run --all-files
```

Die Push-Hooks können manuell getestet werden:

```bash
py -m pre_commit run --hook-stage pre-push --all-files
```

## Aufgabe 4

### Azure-Deployment

Die Anwendung wurde als Azure App Service bereitgestellt.

URL der laufenden Anwendung:

https://zehnderjanlb324-bumblefox-cyhtd4hxcscbexcn.switzerlandnorth-01.azurewebsites.net

### Passwort aus der lokalen `.env` auf Azure übertragen

Lokal befindet sich das Passwort in der Datei `.env`:

```env
PASSWORD="..."
```

Die Datei `.env` wird durch `.gitignore` nicht in das GitHub-Repository eingecheckt.

Für Azure wurde das Passwort als Umgebungsvariable hinterlegt:

1. Azure App Service öffnen.
2. Unter **Einstellungen → Umgebungsvariablen** eine neue App-Einstellung erstellen.
3. Als Name `PASSWORD` eintragen.
4. Als Wert den für die LB vorgegebenen Wert verwenden.
5. Die Einstellung mit **Anwenden** speichern.

Dadurch steht `PASSWORD` der Anwendung auf Azure als Umgebungsvariable zur Verfügung, ohne dass das Passwort im Repository gespeichert werden muss.

### Automatisches Deployment

Das automatische Deployment wurde im Azure-Bereitstellungscenter mit GitHub Actions eingerichtet.

Verwendete Konfiguration:

- Organisation: `BUMBLEFOX-lol`
- Repository: `ZehnderJanLB-324`
- Branch: `main`
- Runtime: Python 3.14
- Authentifizierung: OIDC mit benutzerseitig zugewiesener Identität

Azure hat dafür den Workflow

`.github/workflows/main_zehnderjanlb324-bumblefox.yml`

erstellt.

Der Workflow wird bei jedem Push auf `main` automatisch ausgeführt. Dadurch löst auch ein erfolgreicher Merge nach `main` automatisch ein neues Deployment auf Azure aus.