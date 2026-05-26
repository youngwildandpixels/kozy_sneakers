# Design System — The Last Step
> Référence de développement pour le thème Shopify CLI
> Inspiré de thelaststep.fr · Version 2.0

---

## Table des matières
1. [Typographie](#1-typographie)
2. [Couleurs](#2-couleurs)
3. [Espacement](#3-espacement)
4. [Grilles & Layout](#4-grilles--layout)
5. [Composants UI](#5-composants-ui)
6. [Tokens CSS (settings_schema)](#6-tokens-css)
7. [Structure de fichiers Shopify CLI](#7-structure-de-fichiers-shopify-cli)

---

## 1. Typographie

### Font principale
**Overused Grotesk** — grotesque géométrique sans-serif (self-hosted)
Équivalent natif : `Helvetica Neue`, `Arial`

Les 7 fichiers `.woff2` (Light → Black) sont dans [assets/](kozy-theme/assets/) et déclarés via `@font-face` dans `assets/base.css`. Pas d'import Google Fonts, pas de CDN externe.

```css
/* assets/base.css */
@font-face {
  font-family: 'Overused Grotesk';
  font-weight: 400;
  font-display: swap;
  src: url('OverusedGrotesk-Book.woff2') format('woff2');
}
/* ... idem pour 300 (Light), 500 (Medium), 600 (SemiBold), 700 (Bold), 800 (ExtraBold), 900 (Black) */
```

> Note : le poids 400 (regular) s'appelle **Book** dans cette fonte, pas "Regular" (convention de la fonderie).

### Échelle typographique

> `OG` = Overused Grotesk (seule famille du système).

| Token            | Famille  | Poids | Taille  | Line-height | Letter-spacing | Cas       | Usage                              |
|------------------|----------|-------|---------|-------------|----------------|-----------|------------------------------------|
| `--t-display`    | OG       | 700   | 48px    | 1.0         | -1px           | Normal    | H1 collections ("Nouveautés")      |
| `--t-h1`         | OG       | 800   | 32px    | 1.05        | -0.5px         | Normal    | Titres de page, FAQ, Brand story   |
| `--t-h2`         | OG       | 700   | 22px    | 1.1         | 0              | Normal    | Titres de section                  |
| `--t-brand-over` | OG       | 700   | 20px    | 1.0         | 1px            | Uppercase | Overlay sur images (Salomon, Nike) |
| `--t-mega-brand` | OG       | 700   | 17px    | 1.0         | 0              | Normal    | Titres colonnes méga-menu          |
| `--t-nav`        | OG       | 400   | 14px    | 1.0         | 0              | Normal    | Liens navigation principale        |
| `--t-cta`        | OG       | 600   | 13px    | 1.0         | 2px            | Uppercase | Boutons CTA overlay ("DÉCOUVRIR")  |
| `--t-mega-link`  | OG       | 400   | 13px    | 1.0         | 0.3px          | Uppercase | Liens méga-menu (SAMBA, 2002R…)    |
| `--t-product-name`| OG      | 500   | 13px    | 1.3         | 0              | Normal    | Nom produit sur la card            |
| `--t-product-brand`| OG     | 400   | 11px    | 1.0         | 0              | Normal    | Marque au-dessus du nom produit    |
| `--t-price`      | OG       | 400   | 13px    | 1.0         | 0              | Normal    | Prix produit                       |
| `--t-body`       | OG       | 400   | 14px    | 1.6         | 0              | Normal    | Corps de texte, FAQ réponses       |
| `--t-small`      | OG       | 400   | 12px    | 1.4         | 0              | Normal    | Notes, CGV, breadcrumb             |
| `--t-footer-title`| OG      | 700   | 11px    | 1.0         | 1.5px          | Uppercase | Titres colonnes footer             |
| `--t-footer-link`| OG       | 400   | 12px    | 1.8         | 0              | Normal    | Liens footer                       |

### CSS Variables typographie

```css
/* assets/base.css */
:root {
  --font-primary: 'Overused Grotesk', 'Helvetica Neue', Helvetica, Arial, sans-serif;

  /* Tailles */
  --font-size-display: 48px;
  --font-size-h1: 32px;
  --font-size-h2: 22px;
  --font-size-h3: 18px;
  --font-size-nav: 14px;
  --font-size-body: 14px;
  --font-size-product-name: 13px;
  --font-size-small: 12px;
  --font-size-xs: 11px;
  --font-size-badge: 9px;

  /* Graisses */
  --font-weight-light: 300;
  --font-weight-regular: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 600;
  --font-weight-bold: 700;
  --font-weight-extrabold: 800;
  --font-weight-black: 900;
}

body {
  font-family: var(--font-primary);
  font-weight: var(--font-weight-regular);
  font-size: var(--font-size-body);
  line-height: 1.6;
  color: var(--color-black);
  -webkit-font-smoothing: antialiased;
}

h1 { font-size: var(--font-size-display); font-weight: var(--font-weight-black); line-height: 1.0; letter-spacing: -1px; }
h2 { font-size: var(--font-size-h1); font-weight: var(--font-weight-extrabold); line-height: 1.05; }
h3 { font-size: var(--font-size-h2); font-weight: var(--font-weight-bold); }
```

---

## 2. Couleurs

### Palette principale — monochrome strict

| Token CSS              | Valeur    | Usage                                              |
|------------------------|-----------|----------------------------------------------------|
| `--color-black`        | `#000000` | Texte principal, fond header actif, boutons CTA    |
| `--color-white`        | `#FFFFFF` | Fond général, fond nav, fond cartes produit        |
| `--color-gray-100`     | `#F5F5F5` | Fond images produit, fond page collection          |
| `--color-gray-200`     | `#E8E8E8` | Bordures, séparateurs, grid gap produits           |
| `--color-gray-300`     | `#CCCCCC` | Bordures tailles non-sélectionnées, placeholders   |
| `--color-gray-500`     | `#888888` | Texte secondaire (marque produit, breadcrumb, FAQ) |
| `--color-gray-700`     | `#444444` | Liens footer, texte tertiaire                      |
| `--color-footer-bg`    | `#000000` | Fond footer                                        |
| `--color-footer-input` | `#1A1A1A` | Fond champ newsletter dans footer                  |
| `--color-footer-border`| `#333333` | Bordures dans footer                               |
| `--color-footer-link`  | `#999999` | Texte liens footer                                 |
| `--color-promo`        | `#E8001B` | Badge PROMO uniquement (utilisé en rareté)         |

> **Règle stricte** : Aucune couleur d'accentuation autre que le rouge promo. Tout le design est noir/blanc/gris.

### CSS Variables couleurs

```css
/* assets/base.css */
:root {
  --color-black:         #000000;
  --color-white:         #FFFFFF;
  --color-gray-100:      #F5F5F5;
  --color-gray-200:      #E8E8E8;
  --color-gray-300:      #CCCCCC;
  --color-gray-500:      #888888;
  --color-gray-700:      #444444;
  --color-footer-bg:     #000000;
  --color-footer-input:  #1A1A1A;
  --color-footer-border: #333333;
  --color-footer-link:   #999999;
  --color-promo:         #E8001B;
}
```

---

## 3. Espacement

### Système — base 4px

| Token          | Valeur | Usage typique                                |
|----------------|--------|----------------------------------------------|
| `--space-1`    | 4px    | Micro-espacement, gap badges                 |
| `--space-2`    | 8px    | Padding interne petits éléments              |
| `--space-3`    | 12px   | Gap icônes nav, padding taille swatch        |
| `--space-4`    | 16px   | Padding card produit, gap grille mobile      |
| `--space-5`    | 20px   | Padding latéral mobile                       |
| `--space-6`    | 24px   | Gap grille desktop, padding méga-menu        |
| `--space-8`    | 32px   | Espacement entre sections homepage           |
| `--space-10`   | 40px   | Padding latéral desktop, espacement sections |
| `--space-12`   | 48px   | Sections homepage grand espacement           |
| `--space-16`   | 64px   | Sections homepage XL                         |
| `--space-20`   | 80px   | Sections hero, espacement max                |

```css
:root {
  --space-1:  4px;
  --space-2:  8px;
  --space-3:  12px;
  --space-4:  16px;
  --space-5:  20px;
  --space-6:  24px;
  --space-8:  32px;
  --space-10: 40px;
  --space-12: 48px;
  --space-16: 64px;
  --space-20: 80px;
}
```

---

## 4. Grilles & Layout

### Container

```css
:root {
  --container-max:     1280px;
  --container-padding: var(--space-10); /* 40px desktop */
  --container-padding-mobile: var(--space-5); /* 20px mobile */
}

.container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--container-padding);
}

@media (max-width: 768px) {
  .container { padding: 0 var(--container-padding-mobile); }
}
```

### Grille produits

| Breakpoint        | Colonnes | Gap  |
|-------------------|----------|------|
| Desktop `>1024px` | 4        | 1px  |
| Tablet `768-1024px`| 3       | 1px  |
| Mobile `<768px`   | 2        | 1px  |

> **Important** : Le séparateur entre les cards est `1px solid var(--color-gray-200)` obtenu avec `gap: 1px` sur un container avec `background: var(--color-gray-200)`. Pas de `border` sur les cards individuelles.

```css
.product-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1px;
  background-color: var(--color-gray-200);
}

.product-grid .product-card {
  background: var(--color-white);
}

@media (max-width: 1024px) {
  .product-grid { grid-template-columns: repeat(3, 1fr); }
}

@media (max-width: 768px) {
  .product-grid { grid-template-columns: repeat(2, 1fr); }
}
```

### Collection layout (avec sidebar filtres)

```css
.collection-layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  gap: var(--space-8);
  align-items: start;
}

@media (max-width: 1024px) {
  .collection-layout { grid-template-columns: 1fr; }
  /* Filtres deviennent un drawer/modal sur mobile */
}
```

### Header height

| État          | Hauteur |
|---------------|---------|
| Desktop       | 56px    |
| Mobile        | 52px    |

```css
:root {
  --header-height: 56px;
  --header-height-mobile: 52px;
}
```

---

## 5. Composants UI

### 5.1 Header / Navigation

```css
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--color-white);
  border-bottom: 0.5px solid var(--color-gray-200);
  height: var(--header-height);
  display: flex;
  align-items: center;
}

.site-header__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

/* Logo — stencil grid, font black bold */
.site-logo {
  font-family: var(--font-primary);
  font-weight: var(--font-weight-black);
  font-size: 11px;
  line-height: 1.1;
  letter-spacing: 0;
  text-transform: none;
  color: var(--color-black);
  text-decoration: none;
}

/* Liens nav principaux */
.nav-link {
  font-family: var(--font-primary);
  font-size: var(--font-size-nav);
  font-weight: var(--font-weight-regular);
  color: var(--color-black);
  text-decoration: none;
  transition: opacity 0.15s;
}
.nav-link:hover { opacity: 0.6; }

/* Lien "Sneakers" en forme de pill */
.nav-link--pill {
  border: 1px solid var(--color-black);
  border-radius: 20px;
  padding: 4px 14px;
  font-size: 12px;
}
```

### 5.2 Méga-menu

```css
.mega-menu {
  position: absolute;
  top: var(--header-height);
  left: 0;
  right: 0;
  background: var(--color-white);
  border-bottom: 0.5px solid var(--color-gray-200);
  padding: var(--space-8) var(--space-10);
  display: grid;
  grid-template-columns: repeat(4, 1fr) 340px;
  gap: var(--space-8);
  z-index: 99;
}

.mega-menu__brand-title {
  font-size: 17px;
  font-weight: var(--font-weight-bold);
  margin-bottom: var(--space-3);
}

.mega-menu__link {
  display: block;
  font-size: 13px;
  font-weight: var(--font-weight-regular);
  text-transform: uppercase;
  letter-spacing: 0.3px;
  color: var(--color-black);
  text-decoration: none;
  padding: 3px 0;
  transition: opacity 0.15s;
}
.mega-menu__link:hover { opacity: 0.5; }

.mega-menu__voir-tout {
  font-size: 12px;
  text-decoration: underline;
  display: inline-block;
  margin-top: var(--space-2);
}

/* Images éditoriales à droite */
.mega-menu__editorial {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.mega-menu__editorial-img {
  position: relative;
  overflow: hidden;
  flex: 1;
}

.mega-menu__editorial-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.mega-menu__editorial-label {
  position: absolute;
  bottom: var(--space-2);
  left: var(--space-3);
  font-size: 11px;
  font-weight: var(--font-weight-bold);
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--color-white);
}
```

### 5.3 Breadcrumb

```css
.breadcrumb {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 12px;
  font-weight: var(--font-weight-regular);
  color: var(--color-gray-500);
  padding: var(--space-4) 0;
}

.breadcrumb__separator { color: var(--color-gray-300); }

.breadcrumb__current {
  color: var(--color-black);
  font-weight: var(--font-weight-medium);
}
```

### 5.4 Card produit

```css
.product-card {
  background: var(--color-white);
  display: flex;
  flex-direction: column;
}

.product-card__image-wrapper {
  position: relative;
  background: var(--color-gray-100);
  aspect-ratio: 11 / 10;
  overflow: hidden;
}

.product-card__image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  padding: var(--space-4);
  transition: transform 0.3s ease;
}
.product-card:hover .product-card__image-wrapper img {
  transform: scale(1.04);
}

.product-card__badge {
  position: absolute;
  top: var(--space-2);
  left: var(--space-2);
  background: var(--color-black);
  color: var(--color-white);
  font-size: 9px;
  font-weight: var(--font-weight-bold);
  padding: 3px 7px;
  letter-spacing: 0.8px;
  text-transform: uppercase;
}

.product-card__info {
  padding: var(--space-2) var(--space-3) var(--space-3);
}

.product-card__brand {
  font-size: var(--font-size-xs);
  font-weight: var(--font-weight-regular);
  color: var(--color-gray-500);
  margin-bottom: 2px;
}

.product-card__name {
  font-size: var(--font-size-product-name);
  font-weight: var(--font-weight-medium);
  line-height: 1.3;
  color: var(--color-black);
  margin-bottom: var(--space-1);
}

.product-card__price {
  font-size: var(--font-size-product-name);
  font-weight: var(--font-weight-regular);
}

.product-card__price--sale { color: var(--color-black); }

.product-card__price--compare {
  font-size: var(--font-size-xs);
  color: var(--color-gray-500);
  text-decoration: line-through;
  margin-left: var(--space-1);
}
```

### 5.5 Boutons

```css
/* CTAs primaires : pill (border-radius: 9999px) */
/* Éléments UI (swatches taille, inputs) : border-radius: 0 */
.btn {
  font-family: var(--font-primary);
  font-size: 14px;
  font-weight: var(--font-weight-medium);
  border-radius: 9999px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 13px 28px;
  transition: opacity 0.15s, background 0.15s;
  letter-spacing: 0;
  text-decoration: none;
}

/* Primaire — fond noir */
.btn--primary {
  background: var(--color-black);
  color: var(--color-white);
  border: 1.5px solid var(--color-black);
}
.btn--primary:hover { opacity: 0.8; }

/* Secondaire — contour noir */
.btn--secondary {
  background: var(--color-white);
  color: var(--color-black);
  border: 1.5px solid var(--color-black);
}
.btn--secondary:hover {
  background: var(--color-black);
  color: var(--color-white);
}

/* Texte souligné */
.btn--text {
  background: none;
  border: none;
  color: var(--color-black);
  text-decoration: underline;
  padding: 0;
  font-size: 13px;
  font-weight: var(--font-weight-regular);
}

/* Petit — "Voir tout" */
.btn--sm { padding: 8px 16px; font-size: 12px; }

/* CTA hero overlay */
.btn--cta-overlay {
  background: var(--color-white);
  color: var(--color-black);
  border: 1.5px solid var(--color-black);
  font-size: 13px;
  font-weight: var(--font-weight-semibold);
  letter-spacing: 2px;
  text-transform: uppercase;
  padding: 10px 20px;
}
```

### 5.6 Sélecteur de tailles

```css
.size-selector {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(52px, 1fr));
  gap: 4px;
  margin-bottom: var(--space-6);
}

.size-btn {
  font-family: var(--font-primary);
  font-size: 12px;
  font-weight: var(--font-weight-regular);
  padding: 9px 4px;
  text-align: center;
  background: var(--color-white);
  border: 0.5px solid var(--color-gray-300);
  border-radius: 0;
  cursor: pointer;
  transition: background 0.1s, color 0.1s, border-color 0.1s;
}

.size-btn:hover {
  border-color: var(--color-black);
}

.size-btn.is-selected,
.size-btn[aria-checked="true"] {
  background: var(--color-black);
  color: var(--color-white);
  border-color: var(--color-black);
}

.size-btn.is-unavailable {
  color: var(--color-gray-300);
  text-decoration: line-through;
  cursor: not-allowed;
  pointer-events: none;
}

/* Switcher EU / US / UK / CM */
.size-system-switcher {
  display: flex;
  gap: var(--space-2);
  margin-bottom: var(--space-3);
}

.size-system-btn {
  font-size: 12px;
  font-weight: var(--font-weight-regular);
  background: none;
  border: none;
  color: var(--color-gray-500);
  cursor: pointer;
  padding: 0;
  border-bottom: 1px solid transparent;
}
.size-system-btn.is-active {
  color: var(--color-black);
  font-weight: var(--font-weight-semibold);
  border-bottom-color: var(--color-black);
}
```

### 5.7 Filtres sidebar

```css
.filter-sidebar {
  border-right: none; /* pas de bordure droite, séparé du contenu par gap grid */
}

.filter-group {
  border-bottom: 0.5px solid var(--color-gray-200);
}

.filter-group__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-3) 0;
  cursor: pointer;
  font-size: 13px;
  font-weight: var(--font-weight-regular);
  background: none;
  border: none;
  width: 100%;
  text-align: left;
}

.filter-group__chevron {
  font-size: 10px;
  color: var(--color-gray-500);
  transition: transform 0.2s;
}
.filter-group.is-open .filter-group__chevron { transform: rotate(90deg); }

/* Toggle "En stock uniquement" */
.toggle-switch {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-3) 0;
  font-size: 13px;
  border-bottom: 0.5px solid var(--color-gray-200);
}

.toggle-track {
  width: 34px;
  height: 19px;
  background: var(--color-gray-200);
  border-radius: 10px;
  position: relative;
  cursor: pointer;
  transition: background 0.2s;
}
.toggle-track.is-on { background: var(--color-black); }

.toggle-thumb {
  width: 15px;
  height: 15px;
  background: var(--color-white);
  border-radius: 50%;
  position: absolute;
  top: 2px;
  left: 2px;
  transition: left 0.2s;
}
.toggle-track.is-on .toggle-thumb { left: 17px; }
```

### 5.8 Badges

```css
.badge {
  display: inline-block;
  font-family: var(--font-primary);
  font-size: 9px;
  font-weight: var(--font-weight-bold);
  padding: 3px 7px;
  letter-spacing: 0.8px;
  text-transform: uppercase;
  border-radius: 0;
}

.badge--promo { background: var(--color-black); color: var(--color-white); }
.badge--new   { background: var(--color-black); color: var(--color-white); }
.badge--outline {
  background: var(--color-white);
  color: var(--color-black);
  border: 1px solid var(--color-black);
}
```

### 5.9 Section tabs (Bestsellers / Nouveautés)

```css
.section-tabs {
  display: flex;
  gap: var(--space-6);
  border-bottom: 0.5px solid var(--color-gray-200);
  margin-bottom: var(--space-6);
}

.section-tab {
  font-size: 16px;
  font-weight: var(--font-weight-regular);
  color: var(--color-gray-500);
  padding-bottom: 12px;
  cursor: pointer;
  background: none;
  border: none;
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
  transition: color 0.15s;
}
.section-tab.is-active {
  color: var(--color-black);
  font-weight: var(--font-weight-semibold);
  border-bottom-color: var(--color-black);
}
```

### 5.10 Accordéon FAQ

```css
.accordion__item {
  border-bottom: 0.5px solid var(--color-gray-200);
}

.accordion__trigger {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: var(--space-4) 0;
  background: none;
  border: none;
  cursor: pointer;
  text-align: left;
  font-family: var(--font-primary);
  font-size: 13px;
  font-weight: var(--font-weight-medium);
  color: var(--color-black);
}

.accordion__chevron {
  font-size: 14px;
  font-weight: var(--font-weight-light);
  color: var(--color-gray-500);
  transition: transform 0.2s;
  flex-shrink: 0;
  margin-left: var(--space-4);
}
.accordion__item.is-open .accordion__chevron { transform: rotate(180deg); }

.accordion__content {
  display: none;
  padding: 0 0 var(--space-4);
  font-size: var(--font-size-body);
  font-weight: var(--font-weight-light);
  line-height: 1.6;
  color: var(--color-gray-700);
}
.accordion__item.is-open .accordion__content { display: block; }
```

### 5.11 Icônes de confiance (Trust bar)

```css
.trust-bar {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--space-6);
  padding: var(--space-10) 0;
  border-top: 0.5px solid var(--color-gray-200);
  border-bottom: 0.5px solid var(--color-gray-200);
}

.trust-bar__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: var(--space-2);
}

.trust-bar__icon {
  width: 24px;
  height: 24px;
  stroke: var(--color-black);
  stroke-width: 1.3;
  fill: none;
}

.trust-bar__title {
  font-size: 12px;
  font-weight: var(--font-weight-semibold);
}

.trust-bar__subtitle {
  font-size: 11px;
  color: var(--color-gray-500);
  line-height: 1.4;
}

@media (max-width: 768px) {
  .trust-bar { grid-template-columns: repeat(2, 1fr); }
}
```

### 5.12 Footer

```css
.site-footer {
  background: var(--color-footer-bg);
  color: var(--color-white);
  padding: var(--space-12) 0 var(--space-8);
}

.site-footer__grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: var(--space-8);
  margin-bottom: var(--space-8);
}

.footer-col__title {
  font-size: 11px;
  font-weight: var(--font-weight-bold);
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: var(--color-white);
  margin-bottom: var(--space-4);
}

.footer-col__link {
  display: block;
  font-size: 12px;
  font-weight: var(--font-weight-regular);
  color: var(--color-footer-link);
  text-decoration: none;
  margin-bottom: var(--space-2);
  transition: color 0.15s;
}
.footer-col__link:hover { color: var(--color-white); }

/* Newsletter */
.footer-newsletter {
  border-top: 0.5px solid var(--color-footer-border);
  padding-top: var(--space-6);
  margin-bottom: var(--space-8);
}

.footer-newsletter__title {
  font-size: 13px;
  font-weight: var(--font-weight-semibold);
  color: var(--color-white);
  margin-bottom: var(--space-3);
}

.footer-newsletter__form {
  display: flex;
  max-width: 400px;
}

.footer-newsletter__input {
  flex: 1;
  background: var(--color-footer-input);
  border: 0.5px solid var(--color-footer-border);
  border-right: none;
  color: var(--color-white);
  font-family: var(--font-primary);
  font-size: 11px;
  font-weight: var(--font-weight-regular);
  letter-spacing: 1px;
  padding: 10px 14px;
  outline: none;
}
.footer-newsletter__input::placeholder {
  color: #666;
  letter-spacing: 1px;
}

.footer-newsletter__btn {
  background: var(--color-white);
  color: var(--color-black);
  border: none;
  font-family: var(--font-primary);
  font-size: 11px;
  font-weight: var(--font-weight-bold);
  text-transform: uppercase;
  letter-spacing: 1px;
  padding: 10px 16px;
  cursor: pointer;
  transition: opacity 0.15s;
}
.footer-newsletter__btn:hover { opacity: 0.85; }

/* Bottom bar */
.footer-bottom {
  border-top: 0.5px solid var(--color-footer-border);
  padding-top: var(--space-4);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: var(--space-4);
}

.footer-bottom__copy {
  font-size: 11px;
  color: var(--color-footer-link);
}

.footer-bottom__payments {
  display: flex;
  gap: var(--space-2);
  align-items: center;
}

@media (max-width: 768px) {
  .site-footer__grid { grid-template-columns: 1fr 1fr; gap: var(--space-6); }
}
```

### 5.13 Livraison tags (page produit)

```css
.delivery-tags {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
  margin-bottom: var(--space-6);
}

.delivery-tag {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  font-size: 12px;
  font-weight: var(--font-weight-regular);
  color: var(--color-gray-700);
}

.delivery-tag__dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  flex-shrink: 0;
}
.delivery-tag__dot--green  { background: #2DB05D; }
.delivery-tag__dot--orange { background: #F5A623; }
```

---

## 6. Tokens CSS

### settings_schema.json (extrait typographie + couleurs)

> Note : pas de `font_picker` — Overused Grotesk est self-hosted via `@font-face` dans `assets/base.css` (le `font_picker` Shopify ne supporte que la librairie Google Fonts native).

```json
[
  {
    "name": "Typography",
    "settings": [
      {
        "type": "range",
        "id": "font_body_size",
        "label": "Body font size",
        "min": 12,
        "max": 18,
        "step": 1,
        "unit": "px",
        "default": 14
      }
    ]
  },
  {
    "name": "Colors",
    "settings": [
      {
        "type": "color",
        "id": "color_background",
        "label": "Background",
        "default": "#FFFFFF"
      },
      {
        "type": "color",
        "id": "color_text",
        "label": "Text",
        "default": "#000000"
      },
      {
        "type": "color",
        "id": "color_border",
        "label": "Border",
        "default": "#E8E8E8"
      }
    ]
  }
]
```

### Injection des tokens dans theme.liquid

```liquid
{%- comment -%} Dans <head>, après les balises font {%- endcomment -%}
<style>
  :root {
    --font-primary: 'Overused Grotesk', 'Helvetica Neue', Helvetica, Arial, sans-serif;
    --color-black:        #000000;
    --color-white:        #FFFFFF;
    --color-gray-100:     #F5F5F5;
    --color-gray-200:     #E8E8E8;
    --color-gray-300:     #CCCCCC;
    --color-gray-500:     #888888;
    --color-gray-700:     #444444;
    --color-footer-bg:    #000000;
    --color-footer-input: #1A1A1A;
    --color-footer-border:#333333;
    --color-footer-link:  #999999;
    --color-promo:        #E8001B;
    --header-height:      56px;
  }
  {{ settings.font_body | font_face }}
</style>
```

---

## 7. Structure de fichiers Shopify CLI

```
my-theme/
├── assets/
│   ├── base.css                  ← Variables CSS + reset + utilitaires
│   ├── component-header.css
│   ├── component-mega-menu.css
│   ├── component-product-card.css
│   ├── component-product-form.css
│   ├── component-collection-filters.css
│   ├── component-footer.css
│   ├── section-hero.css
│   ├── section-featured-collection.css
│   ├── section-brand-banner.css
│   ├── section-trust-bar.css
│   ├── global.js
│   └── component-mega-menu.js
│
├── config/
│   ├── settings_schema.json       ← Déclaration des tokens (fonts, couleurs)
│   └── settings_data.json
│
├── layout/
│   └── theme.liquid               ← Google Fonts link + injection CSS variables
│
├── sections/
│   ├── header.liquid              ← Nav + méga-menu
│   ├── footer.liquid              ← Footer 4 colonnes + newsletter
│   ├── hero-slideshow.liquid      ← Hero homepage avec CTA
│   ├── featured-collection.liquid ← Bestsellers / Nouveautés avec tabs
│   ├── brand-banners.liquid       ← Salomon / Birkenstock / Nike
│   ├── slides-carousel.liquid     ← Carousel slides horizontales
│   ├── promo-collection.liquid    ← Section Promos
│   ├── essentials-carousel.liquid ← Vêtements Essentials
│   ├── brand-story.liquid         ← Texte + photo équipe
│   ├── stores-map.liquid          ← Nos boutiques Toulouse/Biarritz/Montpellier
│   ├── trust-bar.liquid           ← 4 icônes de confiance
│   └── newsletter.liquid          ← Newsletter seule si hors footer
│
├── snippets/
│   ├── product-card.liquid        ← Card réutilisable
│   ├── breadcrumb.liquid
│   ├── size-selector.liquid
│   ├── delivery-tags.liquid
│   ├── accordion-item.liquid
│   └── icon-*.liquid              ← SVG icons (account, cart, search…)
│
└── templates/
    ├── index.json                 ← Homepage
    ├── collection.json            ← Page collection (filtres + grille)
    ├── product.json               ← Page produit
    ├── page.faq.json              ← Page FAQ
    ├── page.about.json            ← Page À propos
    └── cart.json
```

---

## Rappels clés

| Règle                          | Valeur / Comportement                              |
|--------------------------------|----------------------------------------------------|
| Border-radius boutons/swatches | **0** — aucun arrondi                              |
| Séparateur grille produits     | `gap: 1px` + `background: #E8E8E8` sur le parent  |
| Hover image produit            | `transform: scale(1.04)` sur l'img                 |
| Font smoothing                 | `-webkit-font-smoothing: antialiased`              |
| Images fond                    | `background: #F5F5F5` + `object-fit: contain`      |
| Sticky header                  | `position: sticky; top: 0; z-index: 100`           |
| Nav pill "Sneakers"            | `border-radius: 20px` (exception aux boutons)      |
| Badges position                | `position: absolute; top: 8px; left: 8px`          |
| Prix barré                     | `text-decoration: line-through; color: #888888`    |
| Footer breakpoint              | 4 cols → 2 cols à `768px`                          |
