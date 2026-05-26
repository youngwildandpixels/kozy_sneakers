# Architecture des fichiers

```
my-theme/
├── assets/
│   ├── base.css                       ← Variables CSS globales + reset. NE PAS TOUCHER sans raison
│   ├── component-header.css
│   ├── component-mega-menu.css
│   ├── component-product-card.css
│   ├── component-product-form.css     ← Page produit : tailles, boutons, livraison
│   ├── component-collection-filters.css
│   ├── component-footer.css
│   ├── section-hero.css
│   ├── section-featured-collection.css
│   ├── section-brand-banner.css
│   ├── section-trust-bar.css
│   ├── global.js                      ← Accordéon, tabs, toggle — vanilla JS uniquement
│   └── component-mega-menu.js
│
├── config/
│   ├── settings_schema.json           ← Tokens déclarés ici (font_picker, couleurs)
│   └── settings_data.json
│
├── layout/
│   └── theme.liquid                   ← Injection Google Fonts + CSS variables dans <head>
│
├── sections/
│   ├── header.liquid
│   ├── footer.liquid
│   ├── hero-slideshow.liquid
│   ├── featured-collection.liquid     ← Tabs Bestsellers / Nouveautés
│   ├── brand-banners.liquid           ← Salomon · Birkenstock · Nike
│   ├── slides-carousel.liquid
│   ├── promo-collection.liquid
│   ├── essentials-carousel.liquid
│   ├── brand-story.liquid
│   ├── stores-map.liquid
│   ├── trust-bar.liquid
│   └── newsletter.liquid
│
├── snippets/
│   ├── product-card.liquid            ← Snippet réutilisé partout
│   ├── breadcrumb.liquid
│   ├── size-selector.liquid
│   ├── delivery-tags.liquid
│   ├── accordion-item.liquid
│   └── icon-*.liquid                  ← SVGs inline (account, cart, search, chevron...)
│
└── templates/
    ├── index.json                     ← Homepage
    ├── collection.json                ← Page collection
    ├── product.json                   ← Page produit
    ├── page.faq.json
    ├── page.about.json
    └── cart.json
```
