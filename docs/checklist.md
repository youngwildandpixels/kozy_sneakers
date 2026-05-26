# Pièges à éviter & Checklist avant commit

## Pièges à éviter

| Situation | Ce qu'il NE faut PAS faire | Ce qu'il faut faire |
|-----------|---------------------------|---------------------|
| Ajouter du style global | Écrire dans `base.css` sans concertation | Créer un `component-xxx.css` dédié |
| Modifier la grille produits | Changer `gap` ou ajouter `border` | Respecter le pattern `gap:1px` + bg parent |
| Styliser un bouton | Ajouter `border-radius` | Garder `border-radius: 0` strict |
| Afficher une couleur d'accentuation | Utiliser une couleur autre que #000/gris | Seul `--color-promo` (#E8001B) est autorisé |
| Charger un script externe | `<script src="https://cdn.xxx...">` CDN externe | Télécharger et mettre dans `assets/` |
| Utiliser une font différente | Ajouter une deuxième famille | Overused Grotesk uniquement, changer le poids |
| Écrire du CSS avec valeurs en dur | `color: #000; font-size: 13px` | `color: var(--color-black); font-size: var(--font-size-product-name)` |

---

## Checklist avant commit

- [ ] `shopify theme check` passe sans erreurs
- [ ] Les variables CSS sont utilisées partout (aucune valeur hardcodée)
- [ ] Le composant est responsive (mobile 375px testé)
- [ ] Les images ont `loading="lazy"`, `width` et `height` définis
- [ ] Les liens ont des `aria-label` si l'icône est sans texte
- [ ] Le HTML est sémantique (`<nav>`, `<main>`, `<section>`, `<article>`)
- [ ] Aucun `!important` dans le CSS (sauf override Dawn forcé, commenté)
- [ ] Le schema JSON de la section est complet et documenté
- [ ] Le snippet `product-card.liquid` est utilisé partout (pas de duplication)
