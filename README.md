# 🧱 Lego Deals Tracker

Ce projet, c’est ma manière de transformer une passion (les sets Lego) en un vrai terrain d’analyse : je veux repérer les bonnes affaires, comprendre le marché et décider si un deal vaut vraiment le coup.

L’idée est simple : agréger les promos, comparer les prix et visualiser rapidement ce qui mérite d’être acheté — que ce soit pour collectionner ou investir.

## ✨ Ce que fait l’application

- Récupère des deals Lego depuis des communautés comme Dealabs et Avenue de la Brique.
- Centralise ces deals dans une API locale.
- Affiche une interface web pour trier, filtrer et comparer les offres.
- Met en avant les bonnes réductions, les deals chauds et les offres avec ventes Vinted disponibles.
- Permet de mettre des deals en favoris.

## 🧭 Organisation du dépôt

- `client/v1` : première version d'apprentissage (manipulation de données dans la console).
- `client/v2` : interface web complète (UI + filtres + stats).
- `server` : API Express + scrapers + données JSON (`websites/` et `sources/`).

## 🚀 Démarrage rapide (local)

### 1. Lancer l’API

```bash
cd server
yarn install
node api.js
```

L’API tourne sur `http://localhost:8092` (port défini dans `server/api.js`, variable `PORT`).

### 2. Ouvrir l’interface web

Dans un autre terminal :

```bash
cd client/v2
python3 -m http.server 8000
```

Puis ouvrir `http://localhost:8000` dans le navigateur.

> La logique est dans `client/v2/portfolio.js` (constante `BASE_URL`) : si `window.location.hostname` se termine par `vercel.app`, l’app utilise l’URL déployée (à mettre à jour ici si le déploiement change), sinon `http://localhost:8092`.

## 🧪 (Optionnel) Mettre à jour les données

Le serveur lit les données depuis :

- `server/websites/*.json` (deals)
- `server/sources/vinted.json` (ventes Vinted)

Pour relancer les scrapers (Avenue de la Brique + Dealabs) et réécrire les JSON dans `server/websites/` :

```bash
cd server
yarn install
node sandbox.js
```

Les fichiers JSON sont ensuite écrits dans `server/websites/`.

## 🔌 API (aperçu)

- `GET /deals/search`
  - `limit` : nombre de deals
  - `price` : prix max
  - `date` : date minimale (ISO)
  - `filterBy` : `best-discount` | `most-commented` | `hot-deals`
- `GET /deals/:id`
- `GET /sales/search`
  - `legoSetId` : id du set
  - `limit` : nombre de ventes

## 📝 Licence

[Uncopyrighted](http://zenhabits.net/uncopyright/)
