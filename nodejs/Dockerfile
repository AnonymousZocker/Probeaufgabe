#Base image 
# - Node 22 ist der aktuelle LTS-Zweig (Support bis April 2027)
# - slim auf Debian-Basis — stabil, bekannte Sicherheitspatch-Zyklen
# - Breite Kompatibilität mit nativen npm-Paketen
FROM node:22-slim

RUN addgroup --system app && adduser --system --ingroup app app

# erstellen eines App Ordners 
WORKDIR /app

# Dateien kopieren
COPY --chown=app:app project-nodejs-express-webapp/ .

# Abhängigkeiten installieren
RUN npm ci --omit=dev

# Jetzt erst auf den unprivilegierten User wechseln
USER app

#Port für express
EXPOSE 3000

# Anwendung starten
CMD ["node", "app.js"]