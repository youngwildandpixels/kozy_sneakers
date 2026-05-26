# CLAUDE.md — The Last Step · Shopify Theme

> Lis ce fichier avant toute modification. Consulte les docs/ pour les détails.

---

## Projet

**Client** : The Last Step
**Type** : Thème Shopify custom (Dawn OS 2.0 modifié) via Shopify CLI
**Référence** : https://www.thelaststep.fr/
**Boutique dev** : 8p7wzp-7h.myshopify.com
**Règle d'or** : Reproduire fidèlement le design du site de référence — aucune invention créative.

---

## Stack technique

| Outil               | Détail                                        |
|---------------------|-----------------------------------------------|
| Shopify CLI         | v3.x                                          |
| Thème base          | Dawn (OS 2.0) — modifié                       |
| CSS                 | Vanilla CSS + CSS Custom Properties           |
| JS                  | Vanilla JS minimal — pas de React/Vue/Alpine  |
| Fonts               | Overused Grotesk (self-hosted .woff2 dans assets/) |
| Paiement fractionné | App Alma                                      |
| Newsletter          | Klaviyo                                       |
| Avis                | Judge.me                                      |
| Filtres             | Shopify native Search & Discovery             |

---

## Commandes utiles

```bash
# Développement local (hot reload)
shopify theme dev --store=8p7wzp-7h.myshopify.com

# Push code uniquement — ne touche PAS aux réglages du Theme Editor
shopify theme push --store=8p7wzp-7h.myshopify.com --theme="Kozy_sneakers_dev" --ignore="templates/*"

# Push avec mise à jour des templates (ajouter/retirer une section) — remet à zéro les réglages des sections modifiées
shopify theme push --store=8p7wzp-7h.myshopify.com --theme="Kozy_sneakers_dev"

# Pull l'état distant
shopify theme pull --store=8p7wzp-7h.myshopify.com --theme="Kozy_sneakers_dev"

# Vérifier les erreurs Liquid
shopify theme check
```

> **Règles push — à respecter absolument :**
> - Ne jamais utiliser `--unpublished` — ça crée un nouveau thème à chaque fois.
> - **Toujours utiliser `--ignore="templates/*"` pour les modifs de code** (CSS, Liquid, JS) — sinon les réglages configurés dans le Theme Editor sont écrasés.
> - N'utiliser le push sans `--ignore` que si on ajoute ou retire une section d'une page. Dans ce cas, prévenir que les réglages de la section concernée seront perdus.
> - `config/settings_data.json` est exclu automatiquement via `.shopifyignore` — ne jamais le pusher.

---

## Documentation

| Fichier | Contenu |
|---------|---------|
| [design-system.md](design-system.md) | Typographie, couleurs, espacement, grille, tous les composants CSS |
| [docs/architecture.md](docs/architecture.md) | Arborescence complète du thème |
| [docs/conventions.md](docs/conventions.md) | Conventions Liquid, CSS BEM, JS vanilla, schema section |
| [docs/pages.md](docs/pages.md) | Structure homepage, collection, produit + snippet product-card |
| [docs/checklist.md](docs/checklist.md) | Pièges à éviter + checklist avant commit |

---

## Règles absolues du Design System

> Détails complets dans [design-system.md](design-system.md).

### Typographie
- **Une seule font** : `Overused Grotesk` — poids 300 à 900 (Light→Black), fallback `Helvetica Neue`
- H1 collection : `font-weight: 700; font-size: 48px; letter-spacing: -1px`
- Noms produits : `font-weight: 500; font-size: 13px`
- Navigation : `font-weight: 400; font-size: 14px`

### Couleurs — palette monochrome stricte
- Noir `#000` · Blanc `#FFF` · Gris `#F5F5F5 / #E8E8E8 / #888`
- Seule accentuation autorisée : `#E8001B` pour les badges PROMO
- Fond images produit : `#F5F5F5` · Fond footer : `#000000`

### Boutons & UI
- **CTAs primaires** (hero, newsletter, achat express) : `border-radius: 9999px` (pill)
- **Éléments UI** (swatches taille, inputs, champs) : `border-radius: 0` strict
- Lien "Sneakers" en nav : `border-radius: 20px` (pill)
- Bouton CTA primaire : `background: #000; color: #fff; border: 1.5px solid #000`
- Bouton CTA secondaire : `background: #fff; color: #000; border: 1.5px solid #000`

### Grille produits
- Séparateur cards : `gap: 1px` + `background: #E8E8E8` sur le parent — jamais de `border` sur `.product-card`
- Desktop 4 col · Tablet 3 col · Mobile 2 col
- Image : `aspect-ratio: 11/10` · `object-fit: contain` · `padding: 16px`

### Hover
- Image produit : `transform: scale(1.04)` avec `transition: 0.3s ease`
- Liens : `opacity: 0.6` — jamais de changement de couleur

---

## Règles de code

- CSS : **variables uniquement**, jamais de valeurs en dur (`var(--color-black)` pas `#000`)
- Nommage CSS : **BEM strict** (`.block__element--modifier`, états `.is-open`)
- JS : **vanilla uniquement** — pas de jQuery, pas de frameworks
- Liquid : tags avec tirets `{%- -%}` pour supprimer les espaces inutiles
- Nouveau style global → créer `component-xxx.css`, ne pas toucher `base.css`
- Scripts externes → télécharger dans `assets/`, pas de CDN inline

> Conventions complètes dans [docs/conventions.md](docs/conventions.md).
