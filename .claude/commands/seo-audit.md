Tu es un expert SEO e-commerce. Fais un audit SEO complet de la homepage du thème Shopify holora en utilisant le framework de `seo-master/SKILL.md` et ses références.

## Contexte
- Site : e-commerce TCG (Pokémon, One Piece, cartes à collectionner)
- Thème Shopify custom
- Lire `seo-master/SKILL.md` pour le framework complet
- Références prioritaires : `seo-master/references/audit.md`, `seo-master/references/ecommerce-seo.md`, `seo-master/references/schema-markup.md`

## Fichiers à analyser
Lis ces fichiers dans l'ordre :
1. `layout/theme.liquid` — structure head, meta, schema
2. `templates/index.json` — sections homepage
3. `sections/hero-video.liquid`
4. `sections/collection-slider.liquid`
5. `sections/reviews-slider.liquid`
6. `sections/newsletter-blog.liquid`
7. `sections/faq.liquid`
8. `assets/critical.css` — performance CSS

## Format du rapport

### Score de santé SEO global : X/100

### 1. Findings techniques
Tableau : Problème | Impact (P0-P3) | Preuve | Fix recommandé

### 2. Findings on-page
Tableau : Problème | Impact | Preuve | Fix recommandé

### 3. Findings e-commerce
Tableau : Problème | Impact | Preuve | Fix recommandé

### 4. AI Search readiness (GEO/AEO)
- Bots autorisés dans robots.txt ?
- Structure extractable pour les LLMs ?
- Schema markup présent ?

### 5. Plan d'action priorisé
- 🔴 P0 — Critique (bloque l'indexation)
- 🟠 P1 — High impact (fixes rapides à fort ROI)
- 🟡 P2 — Moyen terme
- 🟢 P3 — Long terme / nice to have

Focus sur les **5 actions les plus impactantes** pour un site TCG e-commerce francophone.
