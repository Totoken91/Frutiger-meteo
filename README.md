# Frutiger Météo

Display météo plein écran façon **Frutiger Aero** — verre, halos, bleus profonds.
Pensé pour tourner en boucle sur un écran (kiosque, TV, cadre) : zéro interaction,
curseur masqué, rotation automatique des vues.

## Lancer

Aucun build, aucune dépendance réseau hormis l'API météo :

- **Double-clic sur `index.html`** (Three.js est embarqué dans `vendor/`), ou
- petit serveur local : `python3 -m http.server 8080` puis `http://localhost:8080`.

En kiosque : `chromium --kiosk --app=file:///chemin/vers/index.html`

## Configuration

En haut de `index.html` :

```js
window.METEO_CONFIG = {
  ville:        "Paris",
  latitude:     48.8566,
  longitude:    2.3522,
  dureeVue:     10,   // secondes par vue
  rafraichissement: 10, // minutes entre deux appels API
};
```

## Ce que ça fait

- **Fond Three.js 100 % génératif** : dégradé animé par shader qui suit la météo
  *et* l'heure réelle (aube, jour, crépuscule, nuit — d'après les heures de
  lever/coucher), couche de nuages très douce en bruit fractal, pluie/neige en
  particules GPU, éclairs pendant les orages. Volontairement sobre et épuré.
- **UI en verre** (DOM + `backdrop-filter`) : 5 vues en rotation ~10 s —
  Maintenant, En détail, Heure par heure, La semaine, Soleil & lune — avec
  transitions flou/échelle et balayage de reflet.
- **Données [Open-Meteo](https://open-meteo.com/)** (gratuit, sans clé),
  rafraîchies toutes les 10 min. Si l'API est injoignable, un **mode démo**
  prend le relais automatiquement (badge discret en bas à droite).
- Icônes météo **SVG générées** (aucune image externe), textes en français,
  1920×1080 (mise à l'échelle automatique sur les autres résolutions).

## Paramètres d'URL (debug)

| Paramètre | Effet |
|---|---|
| `?demo=1` | force le mode démo |
| `?vue=0…4` | fige une vue (0 = Maintenant … 4 = Soleil & lune) |
| `?code=61` | force un code météo WMO (61 pluie, 71 neige, 95 orage…) |
| `?h=23` | force l'heure du fond (jour/nuit/crépuscule) |

## Licences

Three.js (MIT) est embarqué dans `vendor/` — voir `vendor/THREE-LICENSE`.
