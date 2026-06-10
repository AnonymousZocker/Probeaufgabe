#Base image 
# - Basiert auf Debian Bookworm (aktuell, langfristig gepflegt)
# - slim entfernt unnötige Pakete → kleinere Angriffsfläche
# - Regelmäßige Sicherheitsupdates durch das Python-Docker-Team
# - Gute Balance zwischen Größe und Kompatibilität
FROM python:3.12-slim-bookworm
# User anlegen
RUN addgroup --system app && adduser --system --ingroup app app

# behebt fehler mit nutzter ohne Home 
ENV HOME=/tmp

# erstellen eines App Ordners 
RUN mkdir app
WORKDIR /app

# Dateien kopieren
COPY --chown=app:app . .

# Dependencies installieren (noch als root, weil pip systemweit schreibt)
RUN pip install --no-cache-dir -r requirements.txt

# Jetzt erst auf den unprivilegierten User wechseln
USER app

# Port für Gunicorn
EXPOSE 8000

# Anwendung starten
CMD ["node", "app.js"]