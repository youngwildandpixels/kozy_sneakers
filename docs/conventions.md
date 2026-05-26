# Conventions de code

## Liquid

```liquid
{%- comment -%}
  Utiliser les tags avec tiret {%- -%} pour supprimer les espaces blancs inutiles.
  Toujours commenter le but de chaque section en haut du fichier.
{%- endcomment -%}

{%- liquid
  assign product_image = product.featured_image
  assign has_sale = product.compare_at_price > product.price
-%}
```

### Schema de section

```liquid
{% schema %}
{
  "name": "Nom de la section",
  "tag": "section",
  "class": "section",
  "settings": [
    {
      "type": "collection",
      "id": "collection",
      "label": "Collection"
    }
  ],
  "presets": [
    {
      "name": "Nom de la section"
    }
  ]
}
{% endschema %}
```

---

## CSS — BEM strict

```css
/* Block */
.product-card {}

/* Element */
.product-card__image {}
.product-card__info {}
.product-card__name {}
.product-card__price {}

/* Modifier */
.product-card--featured {}
.product-card__price--sale {}
.product-card__price--compare {}

/* State */
.size-btn.is-selected {}
.size-btn.is-unavailable {}
.accordion__item.is-open {}
.filter-group.is-open {}
```

## CSS — Variables uniquement, jamais de valeurs hardcodées

```css
/* ✅ Correct */
.product-card__name {
  font-size: var(--font-size-product-name);
  color: var(--color-black);
  font-weight: var(--font-weight-medium);
}

/* ❌ Interdit */
.product-card__name {
  font-size: 13px;
  color: #000;
  font-weight: 500;
}
```

---

## JS — Vanilla uniquement

```javascript
// ✅ Correct
document.querySelectorAll('.accordion__trigger').forEach((trigger) => {
  trigger.addEventListener('click', () => {
    trigger.closest('.accordion__item').classList.toggle('is-open');
  });
});

// ❌ Interdit — pas de jQuery, pas de frameworks
$('.accordion__trigger').on('click', function() { ... });
```
