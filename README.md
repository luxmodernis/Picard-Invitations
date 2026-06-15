# Invitation — one-pager

Page d'invitation standalone : `index.html` + assets locaux, sans build, sans bundler, **aucune dépendance externe / CDN**.

> **Arborescence d'assets** : wesendapps accepte une arborescence de fichiers, on garde donc les assets en local (police dans `fonts/`, futurs PNG à venir) plutôt que tout inliner. La migration finale se fera en déplaçant le dossier complet.

## Caractéristiques

- **Effet particules dorées** au clic / touch maintenu (canvas plein écran, émission interpolée tous les 4px, gravité + wiggle + fade-out).
- **Curseur custom** doré sur desktop ; support tactile complet (`touchstart/move/end` + `preventDefault`).
- **Parallax au scroll** en JS vanilla (`requestAnimationFrame` + `scrollY`, attribut `data-parallax`).
- **4 sections** : Hero / Invitation / Détails (cards) / Footer, responsive avec breakpoint unique à `768px`.
- **Assets locaux uniquement** : décor en CSS, icônes en SVG inline, police display **Wulkan Display** servie depuis `fonts/` (fallback Georgia serif), corps en system-ui. Aucun CDN ni Google Fonts.

## Personnaliser le contenu

Tout l'éditorial est en clair dans le `<body>` :

- **Hero** : kicker, titre `<h1>`, sous-titre.
- **Invitation** : mot de bienvenue + monogramme (`.monogram`, actuellement `P`).
- **Détails** : 3 cards — *Quand* / *Où* / *Tenue* (remplacer « Date & horaire », « Adresse du lieu », « Dress code »).
- **Footer** : message de clôture + lien RSVP (`mailto:` à compléter avec l'adresse réelle).

Les paramètres des particules se règlent dans l'objet `PARAMS` (densité, taille, vitesse, decay, gravité, wiggle, halo, step).

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
Livraison finale par upload direct du `index.html` (fichier autonome, aucun fichier annexe requis).

## Compatibilité

Safari iOS 15+, Chrome Android, Chrome / Firefox / Safari desktop.
