# Bible Puzzle (version locale)

Un chapitre lu, une pièce posée. 1 189 pièces, 66 livres, 4 zones.

## Lancer l'app

**Test rapide :** double-clique sur `index.html`. Tout fonctionne, sauf l'installation sur l'écran d'accueil.

**Pour l'installer sur un téléphone (PWA) :** héberge le dossier tel quel sur n'importe quel hébergeur statique en HTTPS (GitHub Pages, Netlify, Cloudflare Pages, un simple serveur web). Aucune étape de build.

```bash
# test en local avec un serveur
python3 -m http.server 8000
```

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | Toute l'app (HTML, CSS, JS, plan des livres) |
| `manifest.webmanifest` | Métadonnées d'installation |
| `sw.js` | Cache hors ligne |
| `icon-192.png`, `icon-512.png` | Icônes |

## Règles implémentées (section 4 du document de passation)

- Rythme libre, un livre en cours par zone, changement de livre à tout moment.
- Lecture linéaire : le prochain chapitre est toujours `chapitres lus + 1`.
- Confirmation obligatoire avant la pose ("Confirmer : Matthieu ch. 6 à 8 (3 pièces) ?").
- Annulation de la dernière pose (accueil, ou bouton dans la notification).
- Un livre terminé enregistre `completed_at` et déclenche l'animation de fin de livre.
- Aucune validation de lecture, ton bienveillant, jour de grâce optionnel pour la série.

## Données

Stockées dans le `localStorage` du navigateur, clé `biblepuzzle.v1`. Le journal `reading_log` suit le schéma de la section 5 (`book_id`, `chapter`, `read_at`, `tz_date`, plus un `session` pour l'annulation). Les statistiques sont toutes calculées à partir de ce journal dans `derive()`.

Limites à connaître :

- Les données sont liées à un navigateur et un appareil. Effacer les données du site les supprime.
- L'export JSON (Réglages) sert de sauvegarde et de transfert entre appareils.

## Brancher un backend plus tard

Remplacer `load()` et `save()` (section "Storage") et garder `derive()` inchangé. Le format d'export contient déjà `reading_log` et `user_book`.

## Prochaines étapes suggérées

1. Tester avec quelques jeunes : l'envie de revenir est-elle là ?
2. Remplacer le nuage de points par l'illustration de l'artiste (la logique 1 point = 1 chapitre ne change pas).
3. Ajouter les mécaniques Duolingo et TikTok retenues (rappel doux, partage de la fresque en image).
