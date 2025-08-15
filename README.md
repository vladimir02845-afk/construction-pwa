# MyController – komplet plików
Data pakietu: 2025-08-14 20:46:53 UTC

## Struktura
- controller/app.py — serwer kontrolny (laptop), panel pod `/ui`
- web_ui/index.html — panel WWW
- podserver/app.py — rozbudowany serwer plików z tokenami tymczasowymi
- build/build_all.ps1 — skrypt do budowy .exe (Windows)
- build/installer.iss — skrypt Inno Setup (opcjonalnie)
- systemd/podserver.service — autostart na Ubuntu
- nginx/files.conf — reverse proxy do podserwera (port 6000)
- docs/deploy.sh — szybkie wdrożenie na VPS + HTTPS (nginx+certbot)

## Szybki start (Windows – controller)
```powershell
python -m venv venv
.env\Scripts\Activate.ps1
pip install fastapi uvicorn requests
# edytuj controller/app.py: ustaw PODSERVER_BASE i PODSERVER_ADMIN_TOKEN
python -m uvicorn controller.app:app --host 0.0.0.0 --port 5000
# panel: http://localhost:5000/ui/
```

## Szybki start (Ubuntu – podserver)
```bash
sudo mkdir -p /opt/podserver && cd /opt/podserver
python3 -m venv venv
source venv/bin/activate
pip install flask werkzeug
# skopiuj podserver/app.py i uruchom:
python3 app.py
```
