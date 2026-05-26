# Pages — Structure attendue

## Homepage (`templates/index.json`)

Ordre des sections dans le JSON :
1. `hero-slideshow` — fullwidth, image + CTA centré
2. `featured-collection` — tabs Bestsellers / Nouveautés, carousel 4 produits
3. `brand-banners` — 3 blocs images (Salomon · Birkenstock · Nike)
4. `slides-carousel` — carousel horizontal slides/sandales
5. `editorial-double` — 2 images plein-écran côte à côte (lifestyle)
6. `promo-collection` — section promos + section "Moins de 100€"
7. `essentials-carousel` — vêtements Fear of God Essentials
8. `brand-story` — texte "The Last Step" + image boutique
9. `stores-map` — 3 boutiques (Toulouse · Biarritz · Montpellier)
10. `trust-bar` — 4 icônes Click&Collect / Authentiques / Livraison / SAV
11. `newsletter` — champ email + subscribe (dans footer ou section dédiée)

---

## Page collection (`templates/collection.json`)

- Breadcrumb en haut
- Layout 2 colonnes : sidebar filtres (240px) + grille produits
- Filtres : En stock toggle · Tailles · Marques · Modèles · Couleurs · Prix
- Tri : dropdown en haut à droite
- Pagination : numérotée (1 · 2 · 3 · >)
- Titre de la collection en H1 `font-weight: 700`

---

## Page produit (`templates/product.json`)

```
breadcrumb
├── Galerie images (60%, sticky scroll)           | Info produit (40%)
│   ├── Image principale grande                   │   ├── Marque (petit, lien collection)
│   ├── Miniatures en bas                         │   ├── Titre produit (H1 bold)
│   └── Bouton zoom (+)                           │   ├── SKU (gris, petit)
│                                                 │   ├── Switcher EU / US / UK / CM
│                                                 │   ├── Grille tailles
│                                                 │   ├── Badge stock restant
│                                                 │   ├── Tags livraison (24/48h · 5-12j)
│                                                 │   ├── [Ajouter au panier]
│                                                 │   ├── [Retirer en boutique]
│                                                 │   ├── Bloc Alma (3x/4x)
│                                                 │   └── Accordéons (Description · Entretien · Livraison)
├── Section "Vous aimerez aussi" (4 produits)
├── Section FAQ (accordéon)
└── Trust bar
```

---

## Snippet product-card.liquid

Paramètres attendus :
- `product` : objet product Shopify
- `show_vendor` : boolean (afficher la marque)
- `show_quick_add` : boolean (bouton achat express)

```liquid
{%- comment -%}
  Paramètres attendus :
  - product : objet product Shopify
  - show_vendor : boolean (afficher la marque)
  - show_quick_add : boolean (bouton achat express)
{%- endcomment -%}

<div class="product-card">
  <a href="{{ product.url }}" class="product-card__link">
    <div class="product-card__image-wrapper">
      {%- if product.compare_at_price > product.price -%}
        <span class="badge badge--promo">PROMO</span>
      {%- endif -%}
      <img
        src="{{ product.featured_image | image_url: width: 600 }}"
        alt="{{ product.featured_image.alt | escape }}"
        loading="lazy"
        width="600"
        height="545"
      >
    </div>
    <div class="product-card__info">
      {%- if show_vendor -%}
        <p class="product-card__brand">{{ product.vendor }}</p>
      {%- endif -%}
      <p class="product-card__name">{{ product.title }}</p>
      <div class="product-card__prices">
        <span class="product-card__price product-card__price--sale">
          {{ product.price | money }}
        </span>
        {%- if product.compare_at_price > product.price -%}
          <span class="product-card__price product-card__price--compare">
            {{ product.compare_at_price | money }}
          </span>
        {%- endif -%}
      </div>
    </div>
  </a>
</div>
```
