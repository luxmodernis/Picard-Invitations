# Picard vous invite — one-pager

Invitation immersive **Picard** : un voyage cinématique au scroll (ciel → forêt → révélation), `index.html` + assets locaux, sans build, sans bundler, **aucune dépendance externe / CDN**.

> **Arborescence d'assets** : wesendapps accepte une arborescence de fichiers ; les assets restent en local (`IMG/`, `fonts/`) plutôt qu'inlinés. La migration finale se fait en déplaçant le dossier complet.

## Le parcours (2 écrans)

Le mini-site = **deux écrans empilés** : le **ciel** (en haut) puis la **forêt** (en bas).

1. **Écran 1 — ciel** : `Ciel.png` + `Nuages.png`, logo Picard, « vous invite », pastille « Scrollez pour commencer l'aventure » (`scroll.png`).
2. **Arrivée** : on scrolle → **parallax** (le ciel s'éloigne, les 3 calques de forêt `foret-3/2/1` se posent à des vitesses différentes), puis **le décor se fige**.
3. **Écran 2 — forêt + révélation** : l'orbe (`ORBES.png`) tourne en continu. **Clic maintenu** = jauge : l'orbe **grossit jusqu'à quasi sortir de l'écran** et les **3 textes défilent** — « Cliquez et maintenez » → « Rendez-vous sur la Bon'App, le 31 Août 2026, 11:11 » → « Le compte à rebours est lancé ! Soyez prêts ! ». Relâché trop tôt → la jauge redescend. À 100 %, le final se verrouille (bouton **Recommencer**). Tout se joue **dans la forêt**, sans écran séparé.

Les fonds sont en `background-size: cover` **centré** (remplissent l'écran proprement, pas de tranche tronquée).

## Caractéristiques techniques

- **Particules dorées** au clic / touch (canvas plein écran, émission interpolée tous les 4px, gravité + wiggle + fade-out — objet `PARAMS`).
- **Curseur custom** doré desktop ; tactile complet. `preventDefault` appliqué **uniquement** pendant la scène de révélation pour ne pas bloquer le scroll mobile.
- **Parallax + beats au scroll** en JS vanilla (`requestAnimationFrame` + `scrollY`, progression de la section « stage » en `position: sticky`).
- **Hold-to-charge** : jauge `charge` 0→1, décroît si relâchée, verrouille la révélation à 100 %.
- **Assets locaux** : photos dans `IMG/`, police display **Wulkan Display** depuis `fonts/` (fallback Georgia serif), corps system-ui. Aucun CDN / Google Fonts.

## Personnaliser

Éditorial en clair dans le `<body>` : « vous invite » (hero), « Un nouveau rendez-vous », « Cliquez et maintenez pour révéler », la date `.reveal-date` (**Bon'App, 31 Août 2026, 11:11**), et le final « Soyez prêts ! ».
Réglages d'animation : `PARAMS` (particules) et les constantes `CHARGE_UP` / `CHARGE_DOWN` (vitesse de charge/décharge).

> ⚠️ **Poids des images** : les PNG `IMG/` sont volumineux (~14 Mo au total, `foret-3` ≈ 5 Mo). Avant prod, prévoir une passe d'optimisation (redimensionnement + WebP/AVIF) pour le temps de chargement mobile.

## Développement

Aucune installation. Ouvrir `index.html` dans un navigateur, ou servir le dossier :

```bash
python3 -m http.server 8000
# puis http://localhost:8000
```

## Déploiement

### Vercel
Repo sans framework → Vercel sert `index.html` en statique, **sans configuration**.

1. Pousser le repo sur GitHub.
2. Importer le repo dans Vercel → Deploy.
3. URL de preview à chaque push de branche / PR ; production sur `main`.

Pas de `vercel.json` nécessaire (sauf domaine custom ou redirects).

### wesendapps
Migration finale en déplaçant le dossier complet (`index.html` + `IMG/` + `fonts/`) en conservant l'arborescence relative.

## Compatibilité

Safari iOS 15+, Chrome Android, Chrome / Firefox / Safari desktop.
