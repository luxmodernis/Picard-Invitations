# Picard vous invite — one-pager

Invitation immersive **Picard** : un voyage cinématique au scroll (ciel → forêt → révélation), `index.html` + assets locaux, sans build, sans bundler, **aucune dépendance externe / CDN**.

> **Arborescence d'assets** : wesendapps accepte une arborescence de fichiers ; les assets restent en local (`IMG/`, `fonts/`) plutôt qu'inlinés. La migration finale se fait en déplaçant le dossier complet.

## Le parcours (4 scènes)

1. **Hero — ciel** : `Ciel.png` + `Nuages.png` en parallax, logo Picard, « vous invite », pastille « Scrollez pour commencer l'aventure » (`scroll.png`).
2. **Forêt** : 3 calques de profondeur (`foret-3` fond / `foret-2` milieu / `foret-1` avant-plan) en parallax → « Un nouveau rendez-vous ».
3. **Révélation (clic maintenu)** : l'orbe (`ORBES.png`) tourne en continu ; **maintenir le clic** charge une jauge — l'orbe grossit et la date « Rendez-vous sur la Bon'App, le 31 Août 2026, 11:11 » monte en taille + opacité. Relâché trop tôt → ça redescend. À 100 %, l'écran final se débloque.
4. **Final** : « Le compte à rebours est lancé ! Soyez prêts ! » + bouton **Fermer** (rejoue depuis le début).

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
