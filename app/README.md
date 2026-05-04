# DevOps Demo App

App fil rouge de la formation Coda. Service Node.js minimal, sert de support à tous les TP (J2 PR → J3 CI → J4 Docker/déploiement).

## Endpoints

- `/` — réponse JSON simple
- `/health` — healthcheck HTTP, utile pour les probes de plateforme (Render / Fly / etc.)
- `/metrics` — métriques au format texte

## Commandes

```bash
npm ci
npm test
npm start
docker build -t devops-app:dev .
```
