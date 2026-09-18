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

Erklären Sie hier, wie Sie das Passwort aus Ihrer lokalen `.env` auf Azure übertragen.