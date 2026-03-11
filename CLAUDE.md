# CLAUDE.md — holora-shopify

## Contexte projet
**Holora** est un site e-commerce de vente de cartes à collectionner (TCG).
- Univers principaux : **Pokémon**, **One Piece**, et autres jeux de cartes
- Produits : boosters, displays, cartes gradées, collections complètes
- Clientèle : joueurs et collectionneurs
- Identité visuelle : sombre, premium, avec des touches de violet/holographique — inspirée de l'aspect brillant/holo des cartes TCG

## Infos store
- Store : `mxyzn7-dh.myshopify.com`
- Theme ID dev : `192372277623`

## ⚠️ Règle absolue — Push Shopify
Ne JAMAIS faire `shopify theme push` sans `--only`. Ça écrase `config/settings_data.json` et `templates/*.json`.

```bash
# Toujours pousser uniquement les fichiers modifiés
shopify theme push --store mxyzn7-dh.myshopify.com --theme 192372277623 --only sections/mon-fichier.liquid

# Si plusieurs fichiers
shopify theme push --store mxyzn7-dh.myshopify.com --theme 192372277623 --only sections/a.liquid --only assets/b.css
```

---

## Typographie
- **Font principale** : `CircularStd`, sans-serif (chargée via `assets/critical.css`)
- **Letter-spacing** : `-0.03em` à `-0.05em` selon la taille (plus grand = plus serré)
- **Line-height titres** : `0.95` pour les grands titres hero
- **Poids** : 200 (subtitle léger), 300–400 (corps/titres), 500 (UI), 600–700 (labels)
- **Tailles hero** : `clamp(2.5rem, 6vw, 4rem)` pour les h1, `24px` pour les subtitles
- Chaque retour à la ligne dans un champ texte = retour à la ligne sur le site → toujours utiliser `| newline_to_br`

---

## Palette de couleurs

### Fonds
| Usage | Valeur |
|---|---|
| Page / hero sombre | `#0a0a10`, `#111` |
| Header scrollé | `#242427` |
| Section reviews / dark | `#1a1a1a` |
| Nav mobile | `rgba(15,15,15,0.95)` |
| Cart drawer | `rgba(10,10,16,0.98)` |

### Texte
| Usage | Valeur |
|---|---|
| Principal | `#fff` |
| Secondaire | `rgba(255,255,255,0.65)` |
| Atténué | `rgba(255,255,255,0.4)` |
| Très discret | `rgba(255,255,255,0.3)` |

### Accent violet (couleur signature holora)
| Usage | Valeur |
|---|---|
| Principal | `#7c3aed` |
| Clair | `#a78bfa` |
| Très clair | `#c4b5fd` |
| Gradient CTA | `linear-gradient(135deg, #a78bfa, #7c3aed)` |
| Glow / halo | `rgba(167,139,250,0.5)`, `rgba(124,58,237,0.5)` |
| Liseré nav | `rgba(167,139,250,0.5)` |

### Vert (compte connecté)
- `#22c55e`

### Bordures / séparateurs
- Standard : `rgba(255,255,255,0.08)`
- Discret : `rgba(255,255,255,0.05)`
- Visibl : `rgba(255,255,255,0.2)` à `rgba(255,255,255,0.3)`

---

## Composants UI

### Boutons principaux (`.hero-video__btn--primary`)
- `background: #fff`, `color: #111`
- `border-radius: 999px`, `padding: 0.9rem 2.2rem`
- Holo au hover : `mix-blend-mode: multiply` (conic-gradient violet)

### Boutons glass (`.hero-video__btn--secondary`)
- `background: rgba(255,255,255,0.08)`, `backdrop-filter: blur(24px) saturate(180%)`
- `border: 1px solid rgba(255,255,255,0.25)`
- `box-shadow: inset 0 1px 0 rgba(255,255,255,0.35), 0 4px 24px rgba(0,0,0,0.15)`
- Hover : fond légèrement plus opaque, holo `mix-blend-mode: overlay`

### Pills / tags
- `border-radius: 15px`, glass identique au bouton secondaire
- Hover : `translateY(-1px)` + fond légèrement plus opaque

### Cards (reviews)
- `border: 2px solid #ffffff`, `border-radius: 16px`
- `background: transparent`

### Effet holographique (hover)
- Span `.holo-layer` injecté en JS sur chaque bouton/pill
- Gradient `conic-gradient` violet/purple qui suit la souris via `--holo-x`, `--holo-y`, `--holo-angle`
- Boutons sur fond blanc : `mix-blend-mode: multiply`
- Boutons sur fond sombre : `mix-blend-mode: screen`
- Pills : `mix-blend-mode: overlay`

### Header
- `position: fixed`, `z-index: 200`
- Fond : transparent sur le hero, `#242427` après le hero (`.is-scrolled`)
- **Scroll vers le bas** : logo + actions disparaissent (`opacity: 0`), barre de recherche reste
- **Scroll vers le haut** : tout réapparaît
- Mobile : header entier glisse vers le haut (`translateY(-100%)`) au scroll
- Cart drawer : `z-index: 210` (au-dessus du header)

### Navigation mobile
- Largeur : `min(320px, 85vw)`, slide depuis la droite
- Liseré violet au `.is-open` : `box-shadow: -2px 0 0 rgba(167,139,250,0.5), -12px 0 35px rgba(124,58,237,0.5), -30px 0 60px rgba(109,40,217,0.2)`
- Sous-menus : toggle avec chevron, animation `max-height`
- Footer : lien compte client

---

## Architecture CSS
- `.shopify-section > .full-width` → `grid-column: 1 / -1` (pleine largeur viewport)
- `.shopify-section > *` → `grid-column: 2` (contrainte page-width)
- Variables : `--page-margin`, `--page-width` (dans `snippets/css-variables.liquid`)

## Espacements standards
- Padding section desktop : `4rem 3rem`
- Padding section mobile : `3rem 1rem`
- Gap boutons : `1rem`
- Transitions UI : `0.2s` (hover rapide), `0.3s` (ouverture/fermeture), `0.8s` (fade-in hero)

---

## Sections existantes
- `sections/header.liquid` — header fixe, cart drawer, search overlay, mobile nav
- `sections/hero-video.liquid` — hero plein écran avec vidéo, CTAs, pills catégories
- `sections/collection-slider.liquid` — slider de produits par collection
- `sections/reviews-slider.liquid` — slider d'avis en défilement infini (rAF)
- `sections/newsletter-blog.liquid`
- `sections/faq.liquid`
