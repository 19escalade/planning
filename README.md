# Planning des référents du 19Escalade

Page statique hébergée sur GitHub Pages. Les données restent dans le Google Sheet du club,
lues et écrites par l'application Apps Script (projet `~/planning-19escalade`, déployé avec clasp).

- `index.html` : vue adhérents (lecture + « Je veux grimper ! »), par défaut. `?vue=adherents` reste accepté pour les anciens liens.
- `index.html?vue=referents` : vue référents (inscription aux créneaux).
- `manifest.webmanifest` n'a pas de `start_url` : un raccourci d'écran d'accueil rouvre l'adresse ajoutée (vue adhérents ou référents).
- `API_URL` (en haut du script de `index.html`) : adresse `/exec` du déploiement Apps Script.
  - lecture : `GET API_URL?api=lire` → `{ inscriptions, envies }`
  - écritures : `POST API_URL` en `text/plain` avec `{"action": "ajouter|retirer|grimper|retirerGrimpeur", "data": ...}`
    → `{ ok: true, data }` ou `{ ok: false, erreur }`
- Icônes : `icone-180.png` (écran d'accueil iPhone), `icone-192.png` / `icone-512.png` (manifeste), `favicon-32.png`.
- `.nojekyll` : GitHub Pages sert les fichiers tels quels.

L'ancienne adresse Apps Script (page HTML) continue de fonctionner.

## Mettre à jour

Modifier `index.html`, puis `git commit` et `git push` : GitHub Pages republie en une minute environ.
Si on change le script (Code.js), il faut le redéployer sur le même déploiement (`clasp deploy -i ...`) pour garder la même `API_URL`.
