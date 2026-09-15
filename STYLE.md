# STYLE.md — Charte graphique de La Boussole SEO

Ce document est la référence unique pour tout développement futur du site **La Boussole SEO**. Il décrit précisément le langage visuel du site tel qu'implémenté dans [`styles.css`](styles.css) (fichier CSS unique, appliqué à toutes les pages : accueil, programme, paliers, chapitres). Toute nouvelle page ou composant doit respecter ces règles pour garantir la cohérence visuelle du site.

Le style retenu est un **néo-brutalisme doux** : couleurs vives et franches, contours noirs épais, ombres pleines décalées (sans flou), typographie bold. L'ensemble donne une identité ludique, énergique et très lisible, assumée comme un parti pris graphique fort plutôt qu'un style neutre/corporate.

> Nom de marque : **La Boussole SEO**. Logo : `logo-la-boussole-seo.png` (image), affiché à côté du nom de marque en toutes lettres dans le header (classe `.logo` = image `.logo-mark` 38×38px + texte).

---

## 1. Principes directeurs

1. **Contours francs partout.** Quasiment tous les éléments d'interface (cartes, boutons, badges, tableaux, champs) sont cernés d'une bordure de 2 à 3px dans la couleur `--ink` (quasi-noir), jamais dans une couleur grise neutre.
2. **Ombres pleines, pas de flou.** Les ombres ne sont jamais des `box-shadow` floues (`blur-radius: 0`) : elles simulent un décalage d'aplat façon autocollant/BD (`4px 4px 0 var(--ink)`). Elles s'accentuent légèrement au survol.
3. **Micro-interactions "pressées".** Au survol, les éléments interactifs se décalent visuellement vers le haut-gauche (`translate(-1px,-1px)` à `translate(-2px,-2px)`) et l'ombre grandit ; au clic/`:active`, ils se décalent vers le bas-droite et l'ombre se réduit — évoquant un bouton physique qu'on enfonce.
4. **Couleurs vives en aplat, jamais de dégradé.** Violet, jaune, vert menthe : des couleurs franches et saturées, posées en blocs pleins.
5. **Emoji comme iconographie.** Le site n'utilise aucune librairie d'icônes SVG : les pictogrammes sont des emojis Unicode insérés directement dans le texte (🎓 ✅ 🧩 ⏱️ 📖 🟢 🟡 🔴 🟣 💡 ⚠️). C'est un choix délibéré de légèreté technique, à conserver pour toute nouvelle page plutôt que d'introduire une librairie d'icônes.
6. **Typographie bold assumée.** Les poids de police vont rarement sous 600 ; le corps de texte lui-même est en 400 mais tous les libellés d'UI (nav, boutons, badges, métadonnées) sont en 700–800.

---

## 2. Couleurs

Toutes les couleurs sont déclarées en variables CSS dans `:root` (haut de [`styles.css`](styles.css)). **Ne jamais coder une couleur en dur** dans un nouveau composant : toujours passer par une variable existante, ou en créer une nouvelle dans `:root` si un vrai besoin apparaît.

### 2.1 Palette de base (neutres et surfaces)

| Variable | Valeur hex | Usage |
|---|---|---|
| `--bg` | `#f4f1ff` | Fond de page général (lavande très clair) |
| `--bg-soft` | `#ebe6ff` | Fonds secondaires : encarts, lignes de tableau au survol, cartes de progression |
| `--surface` | `#ffffff` | Cartes, blocs de contenu, boutons par défaut — la surface "au-dessus" du fond |
| `--ink` | `#15122b` | Texte principal, bordures, fonds sombres (header trust-band, hook-block) |
| `--ink-soft` | `#46406b` | Texte secondaire (paragraphes, nav) |
| `--ink-faint` | `#8680ab` | Texte tertiaire (métadonnées, légendes, placeholders) |
| `--border` | `#15122b` | Couleur de bordure standard — **identique à `--ink`**, c'est la signature visuelle "contour noir" du site |

### 2.2 Couleurs de marque

| Variable | Valeur hex | Usage |
|---|---|---|
| `--brand` | `#5b2ee8` | Violet vif — couleur d'identité principale (liens actifs, barres de progression, numéros d'étape, liens jargon) |
| `--brand-dark` | `#3d1cb0` | Violet foncé — texte de code/exemple, valeurs mises en avant dans les tableaux jargon |
| `--brand-soft` | `#e7e0ff` | Fond teinté violet clair (chips, item TOC actif, `.measure-card`) |
| `--accent` | `#ffb703` | Jaune franc — couleur du **bouton primaire / CTA**, l'appel à l'action visuel numéro 1 du site |
| `--accent-dark` | `#d99600` | Jaune foncé (réservé — pas encore utilisé activement dans le CSS actuel, prévu pour un état hover accent) |
| `--accent-soft` | `#fff2d2` | Fond jaune clair (encarts "analogie", encarts "piège/pitfall") |
| `--mint` | `#05d19c` | Vert menthe — badge "eyebrow" du hero, coches ✓ de la liste d'objectifs |

### 2.3 Couleurs sémantiques "paliers"

Le site organise son contenu en 10 paliers (0 à 9), regroupés en 4 niveaux de couleur qui servent aussi de code sémantique **succès / attention / erreur / spécial** :

| Groupe | Paliers | Couleur texte | Couleur fond | Sens |
|---|---|---|---|---|
| Vert | 0, 1, 2, 3, 4 | `--palier-0` `#05a97a` | `--palier-0-bg` `#d3f7ea` | Débutant / fondamentaux — aussi utilisé comme couleur de **succès** (`.quiz-option.correct`, `.status-published`) |
| Jaune | 5, 6 | `--palier-5` `#e0a300` | `--palier-5-bg` `#fff0c2` | Intermédiaire |
| Rouge/rose | 7, 8 | `--palier-7` `#f0355b` | `--palier-7-bg` `#ffdbe4` | Avancé — aussi utilisé comme couleur d'**erreur** (`.quiz-option.incorrect`) |
| Violet | 9 | `--palier-9` `#5b2ee8` | `--palier-9-bg` `#e7e0ff` | GEO / spécial (= identique à `--brand`) |

Ces couleurs pilotent : le badge numéroté de chaque palier (`.palier-num`, `.badge`), le tag de chapitre (`.palier-tag`), les puces emoji 🟢🟡🔴🟣 associées dans le HTML, et le statut de publication d'un chapitre.

### 2.4 États d'interface

- **Succès** (quiz correct) : fond `--palier-0-bg`, pastille pleine `--palier-0` + texte blanc.
- **Erreur** (quiz incorrect) : fond `--palier-7-bg`, pastille pleine `--palier-7` + texte blanc.
- **Statut publié** (`.status-published`) : fond `--palier-0-bg`, texte `--ink`.
- **Statut brouillon** (`.status-draft`) : fond `--bg-soft`, texte `--ink-faint`.
- **Désactivé** (`.chapter-row.disabled`) : `opacity: 0.7`, texte en `--ink-faint`, curseur par défaut, pas de survol.
- **Hover générique** : accentuation de l'ombre (`--shadow` → `--shadow-hover`) + léger décalage `translate(-1px,-1px)` à `translate(-2px,-2px)`.
- **Active/pressed** : décalage inverse `translate(2px,2px)`, ombre réduite à `1px 1px 0 var(--ink)`.
- **Désactivé (bouton)** : `.btn[disabled]` → `opacity: 0.5; cursor: not-allowed; pointer-events: none;`, sans effet de survol/clic. Utilisé pour les CTA menant à un chapitre pas encore publié (voir 5.1 et 11).
- **Focus** : non stylé explicitement dans le CSS actuel (à traiter en priorité — voir section 9, Points d'attention).

Il n'existe **pas de mode sombre** sur le site (à l'exception des bandes intentionnellement sombres `.trust-band` et `.hook-block`, qui sont des choix de mise en page, pas un thème global).

### 2.5 Ombres et bordures — tokens dédiés

| Variable | Valeur | Usage |
|---|---|---|
| `--radius-s` | `6px` | Petits éléments : boutons, badges, chips, inputs |
| `--radius-m` | `10px` | Cartes standards (palier-card, example-card, jargon-table) |
| `--radius-l` | `16px` | Grands blocs : hero-art, hook-block, quiz-block, next-card, practice-block |
| `--shadow` | `4px 4px 0 var(--ink)` | Ombre "au repos" — aplat plein décalé bas-droite, sans flou |
| `--shadow-hover` | `6px 6px 0 var(--ink)` | Ombre au survol — même principe, décalage plus prononcé |

Bordures : quasi systématiquement `2px` à `3px solid var(--border)` ; `1.5px` sur les petits éléments (légende, badge de statut) ; `2px dashed` pour les séparateurs internes discrets (lignes de chapitre dans la liste programme, étapes de practice-block).

---

## 3. Typographie

### 3.1 Polices

Chargées via Google Fonts (`<link>` dans le `<head>` de chaque page, jamais en self-hosted) :

- **Titres** (`--font-serif`) : **Space Grotesk**, poids 500/600/700. Fallback `"Segoe UI", system-ui, sans-serif`.
- **Corps de texte** (`--font`) : **DM Sans**, poids 400/500/700/800. Fallback `"Segoe UI", system-ui, -apple-system, sans-serif`.
- **Code / extraits techniques** : `"Cascadia Code", Consolas, monospace` (blocs `<pre>` et `<code>` inline).

Malgré le nom de la variable, `--font-serif` désigne la police de titres (Space Grotesk, une sans-serif géométrique) — le nom est un héritage historique du fichier, pas une police avec empattements. À conserver tel quel pour ne pas casser la cohérence avec le CSS existant, mais à noter pour ne pas s'y méprendre.

### 3.2 Échelle et règles

- **Corps** : `body { font-size: 16px; line-height: 1.6; }`
- **Titres** (`h1-h4`) : `font-family: var(--font-serif); font-weight: 700; line-height: 1.15; letter-spacing: -0.01em;` — resserrés, jamais en majuscules par défaut.
- **H1 hero** : `clamp(2.2rem, 4.2vw, 3.3rem)` — fluide entre mobile et desktop.
- **H2 de section** (`.section-head h2`) : `clamp(1.7rem, 3vw, 2.3rem)`.
- **H1 page chapitre** : `clamp(1.9rem, 3.5vw, 2.6rem)`.
- **H1 page programme** (`.page-hero h1`) : `clamp(1.9rem, 3.6vw, 2.5rem)`.
- **Paragraphes** : `color: var(--ink-soft)`, `margin-bottom: 1em`.
- **Liens** : `color: inherit; text-decoration: none;` par défaut — la couleur/le style de survol est défini au cas par cas selon le contexte (nav, breadcrumb, footer).
- **Boutons** : `font-weight: 800`, `font-size: 0.95rem` (0.85rem en variante `.btn-sm`) — jamais de majuscules forcées.
- **Libellés/badges** ("eyebrow", "status", "legend-dot", labels de `.next-card`) : `font-size: 0.7–0.85rem`, `font-weight: 800`, souvent `text-transform: uppercase` + `letter-spacing: 0.02–0.04em`.
- **Code inline** (`code`) : `font-size: 0.92em`, fond `--bg-soft`, bordure `1.5px solid var(--border)`, `border-radius: 4px`, padding `1px 6px`.
- **Blocs de code** (`.example-card pre`) : `font-size: 0.86rem` (réduit à `0.74rem` sous 960px), couleur `--brand-dark`, fond `--surface`.

---

## 4. Espacements et mise en page

Pas de tokens d'espacement formalisés (`--space-*`) : les valeurs sont posées directement en px, mais suivent une logique cohérente d'un composant à l'autre.

- **Conteneur global** : `.container { max-width: 1120px; margin: 0 auto; padding: 0 24px; }` — c'est la seule règle de largeur maximale du site, à réutiliser pour toute nouvelle section.
- **Padding vertical de section** : `section { padding: 60px 0; }`, réduit à `40px 0` sous 640px.
- **Hero** : `padding: 72px 0 56px` (desktop) → `44px 0 36px` (mobile).
- **Gaps de grilles** : `16–24px` selon densité (`.palier-grid` 20px, `.steps` 24px, `.trust-stats` 16px) ; `.hero .container` et `.chapter-layout` : `48px`.
- **Padding intérieur des cartes** : `.palier-card` 22px, `.hook-block`/`.practice-block`/`.quiz-block` 30–32px, `.measure-card`/`.example-card pre` 20px.

### Breakpoints responsive

| Breakpoint | Effet |
|---|---|
| `max-width: 960px` | Grilles passent de 3/4 colonnes à 1/2 colonnes (`.hero`, `.palier-grid`, `.steps`, `.trust-band`) ; `.chapter-layout` (sidebar TOC 230px + contenu) passe en 1 colonne ; la TOC de chapitre (`.chapter-toc`) devient une barre horizontale scrollable (sticky → static, `flex-direction: row`) ; le code des `.example-card pre` réduit sa taille de police et passe en retour à la ligne. |
| `max-width: 860px` | Bascule du header en **mode mobile** : `.main-nav` et `.btn-sm` disparaissent, `.nav-toggle` (bouton hamburger) apparaît. |
| `min-width: 861px` | Force le masquage du panneau `.mobile-nav` même s'il a été ouvert juste avant le redimensionnement. |
| `max-width: 640px` | Grilles à 1 colonne (`.palier-grid`, `.steps`), padding de section réduit, hero compacté. |

---

## 5. Composants UI

### 5.1 Boutons (`.btn`)

- Base : `padding: 12px 22px; border-radius: var(--radius-s); font-weight: 800; font-size: 0.95rem;` + double ombre `box-shadow: 0 0 0 2px var(--border), var(--shadow);` (le contour et l'ombre décalée sont deux couches distinctes).
- **`.btn-primary`** : fond `--accent` (jaune), texte `--ink`. C'est le CTA principal du site — "Commencer gratuitement", "Découvrir le premier chapitre", "Continuer".
- **`.btn-ghost`** : fond `--surface` (blanc), texte `--ink` — CTA secondaire ("Voir le programme complet", "Refaire le quiz"). Au survol, fond `--brand-soft`.
- **`.btn-sm`** : variante compacte pour le header (`padding: 9px 16px; font-size: 0.85rem`).
- **`.btn[disabled]`** : variante désactivée (bouton HTML natif avec l'attribut `disabled` + `aria-disabled="true"`, pas un lien `<a>`), utilisée pour un CTA qui mène à un chapitre non encore publié — voir 11. Toujours accompagnée d'un libellé qui l'indique clairement (ex. "À venir", "Chapitre suivant — à venir") plutôt que du texte d'action habituel ("Continuer →").
- Interaction : survol = ombre agrandie + `translate(-1px,-1px)` ; clic (`:active`) = décalage inverse `translate(2px,2px)` + ombre réduite à `1px 1px 0 var(--ink)`.

### 5.2 Cartes

Toutes les cartes partagent le même socle visuel : `background: var(--surface); border: 2–2.5px solid var(--border); border-radius` variable selon la taille ; `box-shadow: var(--shadow)` ; hover → `var(--shadow-hover)` + léger décalage.

- **`.palier-card`** : carte cliquable de la grille d'accueil, badge numéroté coloré (`.palier-num`) selon le groupe de couleur du palier.
- **`.example-card`** : bloc de code avec barre de titre (`.example-bar`, fond `--bg-soft`) façon fenêtre d'éditeur.
- **`.analogy-card`** : encart pédagogique, fond `--accent-soft`, **bordure gauche épaisse** (`border-left: 6px solid var(--accent)`) qui le distingue visuellement d'une carte standard.
- **`.measure-card`** : encart "à retenir", fond `--brand-soft`.
- **`.next-card`** : carte de transition "chapitre suivant", avec une ligne d'en-tête `.next-card-prev-row` (fond `--bg-soft`) séparée du corps par une bordure.
- **`.hook-block`** : bloc d'ouverture de chapitre, **fond sombre** `--ink` avec texte blanc et ombre colorée `6px 6px 0 var(--brand)` — seul bloc de contenu à inverser le contraste.
- **`.practice-block`** : fond `--bg-soft`, contient une suite de `.practice-step` séparées par des bordures pointillées.

### 5.3 Badges et pastilles

- **`.chip`** : fond `--brand-soft`, bordure 2px, `border-radius: var(--radius-s)`, `font-weight: 800`.
- **`.status-published` / `.status-draft`** : pastille uppercase, `border-radius: var(--radius-s)`, `letter-spacing: 0.02em`.
- **`.palier-tag`** : tag de contexte en tête de page chapitre, fond coloré selon palier.
- **`.legend-dot`** : légende couleur du programme (petit carré 12×12px avec bordure).
- **`.tick`** : coche ronde (✓/1/2/3…) des listes d'objectifs et étapes, fond `--mint`, `border-radius: 50%`.

### 5.4 Formulaires / Quiz

- **`.quiz-block`** : conteneur principal, bordure 3px, `box-shadow: 6px 6px 0 var(--ink)` (ombre renforcée par rapport aux cartes standards, pour signaler l'interactivité).
- **`.quiz-option`** : ligne cliquable, bordure 2.5px, hover → décalage + ombre `3px 3px 0 var(--ink)`.
  - État **`.correct`** : fond `--palier-0-bg`, pastille lettre pleine `--palier-0`.
  - État **`.incorrect`** : fond `--palier-7-bg`, pastille lettre pleine `--palier-7`.
  - État désactivé après réponse : `[aria-disabled="true"]` → `cursor: default`.
- **`.quiz-explain`** : encart d'explication, masqué par défaut (`display: none`), affiché via classe `.visible` après réponse.
- **`.progress-track` / `.progress-fill`** : barre de progression pilule (`border-radius: 999px`), remplissage en `--brand`.
- **`.quiz-score .score-num`** : score final, très grand (`2.8rem`), en police de titre, couleur `--brand`.

### 5.5 Navigation / Header

- **`.site-header`** : sticky (`top: 0; z-index: 50;`), fond `--bg` uni (pas de flou/transparence), bordure basse épaisse 3px — cohérent avec le principe "contour franc partout".
- **`.logo`** : image `.logo-mark` (38×38px, `object-fit: contain`) + texte du nom de marque en police de titre.
- **`.main-nav a.active`** : soulignement via `::after`, barre `3px` en `--brand` sous le lien actif.
- **Menu hamburger** (`.nav-toggle` + `.mobile-nav`) : seul mécanisme de navigation mobile du site, actif sous 860px. Bouton carré 42×42px avec 3 barres qui s'animent en croix à l'ouverture (`transform: translateY + rotate`, `opacity`) ; panneau déroulant sous le header (`position: absolute; top: 100%`) avec la même ombre pleine caractéristique (`box-shadow: 0 8px 0 var(--ink)`). Piloté par un petit script inline (toggle de classe `.open`), présent en double sur chaque page (accueil + pages chapitre) — voir section 9.
- **`.chapter-toc`** : sommaire latéral sticky (page chapitre), item actif = bordure gauche `--brand` + fond `--brand-soft`, mis à jour dynamiquement via `IntersectionObserver` au scroll.
- **`.breadcrumb`** : fil d'Ariane, séparateurs `/`, liens en `--ink-soft` → `--ink` au survol.

### 5.6 Footer

`.site-footer` : bordure haute épaisse 3px, `padding: 36px 0`, disposition `flex` avec mention légale à gauche et `.footer-links` à droite (passent en colonne empilée si l'espace manque, via `flex-wrap`).

### 5.7 Tableaux

`.jargon-table` : bordure externe épaisse (2.5px), en-tête `<th>` en fond `--ink` / texte blanc uppercase, première colonne (`td:first-child`) mise en avant en `--brand-dark` + police de titre.

---

## 6. Layout

- **Système de grille** : CSS Grid natif (`display: grid; grid-template-columns: repeat(n, 1fr)`), pas de framework externe.
- **Largeur max de contenu** : `1120px` (`.container`), avec des sous-contraintes locales : `.chapter-body { max-width: 720px }`, `.chapter-hero-grid { max-width: 998px }`, `.programme-list .container { max-width: 950px }`.
- **Page chapitre** : disposition à 2 colonnes — TOC latérale fixe (`230px`) + corps de contenu (`1fr`), `gap: 48px`. Passe en 1 colonne sous 960px, la TOC devenant une barre horizontale.
- **Accordéons natifs** : le programme utilise `<details>`/`<summary>` (`.palier-block`) sans JavaScript, avec un chevron animé en pur CSS (`transform: rotate(180deg)` sur `[open] .chev`).
- **Hero** : grille 2 colonnes (`1.1fr 0.9fr`) → 1 colonne sous 960px.

---

## 7. Iconographie

**Aucune librairie d'icônes SVG** (pas de Font Awesome, Lucide, Feather...). Toute l'iconographie du site passe par des **emojis Unicode** intégrés directement dans le texte HTML :

| Emoji | Usage |
|---|---|
| 🎓 | Badge "Formation gratuite" |
| ✅ | Point de confiance ("aucun compte requis"), quiz |
| 🧩 | Métadonnée "prérequis" / nombre de paliers |
| ⏱️ | Temps de lecture estimé |
| 📖 | Nombre de chapitres |
| 🟢 🟡 🔴 🟣 | Code couleur des paliers (débutant → avancé → GEO) |
| 💡 | Encart "analogie" ou explication de quiz |
| ⚠️ | Encart "piège fréquent" |
| 🌐 | Icône de barre "fenêtre de code" |

Ces emojis sont insérés en dur dans le HTML, pas via CSS `content`, et **héritent de la police système** (non recolorables, taille liée au `font-size` du conteneur parent). Pour toute nouvelle page, conserver ce principe plutôt que d'introduire une dépendance à une librairie d'icônes.

---

## 8. Images et logo

- **Logo** : `logo-la-boussole-seo.png`, affiché en 38×38px (`object-fit: contain`) dans le header, toujours accompagné du nom de marque "La Boussole SEO" en texte à côté (jamais le logo seul).
- **Images de contenu** : règle générique `img { max-width: 100%; }` uniquement — pas de traitement automatique (pas de `border-radius` ni d'ombre par défaut sur une balise `<img>` isolée). Les seuls éléments visuellement traités (bordure/radius/ombre) sont les conteneurs de type carte qui encadrent du contenu (`.hero-art`, `.example-card`), pas les images brutes.
- Pas de ratio d'image imposé (`aspect-ratio` non utilisé dans le CSS).

---

## 9. Points d'attention pour les développements futurs

- **États `:focus` non stylés.** Le CSS actuel ne définit aucun style de focus visible (clavier) pour les liens, boutons et options de quiz — à corriger en priorité pour l'accessibilité avant toute mise en production plus large.
- **Script de menu mobile dupliqué.** Le script inline qui pilote `.nav-toggle` / `.mobile-nav` est copié-collé dans chaque page HTML plutôt que centralisé dans un fichier JS partagé (`quiz.js` existe déjà pour la logique de quiz — le même principe pourrait s'appliquer à la nav).
- **`--font-serif` n'est pas une police à empattements** (c'est Space Grotesk, une sans-serif) : le nom de variable est trompeur mais ne doit pas être renommé sans vérifier tous les usages dans `styles.css`.
- **Emoji comme seule iconographie** : fonctionne bien pour l'instant, mais leur rendu varie selon l'OS/navigateur (Windows, macOS, Android) — à surveiller si le site grandit et qu'un rendu pixel-perfect devient nécessaire.
- **Pas de mode sombre global** : `.trust-band` et `.hook-block` sont des blocs sombres isolés dans une page globalement claire, pas un thème alternatif activable.

---

## 10. Du document source (Markdown) au chapitre HTML

Chaque chapitre part d'un document source au format Markdown (ex. `Chapitre 6 — Le rendu JavaScript et le crawl budget.md`) et devient une page `palier-X/chapitre-Y/index.html`. Cette section documente précisément cette conversion, établie par comparaison ligne à ligne entre un document source et sa page HTML publiée (`palier-1/chapitre-6/index.html`).

La conversion n'est **pas purement mécanique** : une partie des règles est un mapping direct Markdown → HTML, une autre partie nécessite de compléter des éléments absents du document (titres de blocs fixes, explications de quiz). Les deux types de règles sont distingués ci-dessous.

> **Règle prioritaire : reformulation minimale.** Le texte du document source doit être repris **verbatim** dans le HTML de sortie, au mot près, chaque fois que c'est possible. Fusionner des lignes courtes ou des puces en un paragraphe fluide (bloc Accroche, listes aplaties en prose) est une opération de **mise en forme** — ne pas en profiter pour reformuler les phrases, changer des mots, résumer ou "améliorer" le style : on ne fait que retirer les puces/retours à la ligne et ajuster la ponctuation de jonction (`;` → `,`, ajout d'un point final), jamais réécrire le fond. La réécriture ou l'ajout de texte (voir 10.6) doit rester l'exception, strictement limitée aux endroits où le gabarit HTML exige un élément qui n'existe dans le document sous aucune forme (ex. le `<h3>` de l'accroche, l'explication d'une bonne réponse de quiz). Dans tous les autres cas, en cas de doute entre reformuler et copier tel quel, toujours copier tel quel.

### 10.1 Emplacement et nommage du fichier de sortie

- Le titre du document source commence par `# Chapitre N — Titre du chapitre`. Le numéro `N` et le palier annoncé juste en dessous (`Palier P — Nom du palier (sous-titre)`) déterminent le chemin de sortie : `palier-P/chapitre-N/index.html`.
- Toutes les URLs internes de la page (logo, nav, styles.css, images, quiz.js) sont **relatives** et remontent à la racine avec `../../` depuis un chapitre (`palier-P/chapitre-N/`) — à ne jamais transformer en chemins absolus.
- Le lien "Chapitre précédent"/"Chapitre suivant" pointe vers `../chapitre-{N-1}/` et `../chapitre-{N+1}/` (dans le même palier).

### 10.2 Correspondances mécaniques Markdown → HTML

| Markdown source | HTML de sortie | Remarque |
|---|---|---|
| `\<title\>X\</title\>` (ligne d'en-tête du doc) | `<title>X</title>` | Repris verbatim dans le `<head>`, désenchappé des `\` |
| `\<meta name="description" content="..."/\>` | `<meta name="description" content="...">` | Le slash de fermeture `/>` disparaît (balise HTML void classique) |
| `**texte en gras**` | `<strong>texte en gras</strong>` | Mapping direct |
| `### Sous-titre` | `<h3>Sous-titre</h3>` | Mapping direct **quand le sous-titre existe déjà dans la source** — voir 10.4 pour les cas où un `<h3>` est ajouté par l'éditeur |
| `| Terme | Définition |` (tableau Markdown) | `<table class="jargon-table"><tr><th>Terme</th><th>Définition</th></tr>...</table>` | Ligne d'en-tête → `<th>`, lignes suivantes → `<td>`, la ligne de séparation `\| ----- \|` est supprimée. Pas de `<thead>`/`<tbody>`, des `<tr>` à plat. |
| `---` (ligne de séparation horizontale entre sections) | *(rien)* | Purement un repère visuel dans le document source ; jamais traduit en `<hr>` ni conservé dans le HTML |
| Apostrophe typographique `’` | Apostrophe droite `'` | Normalisation systématique dans tout le texte de sortie (titres, meta description, corps de texte) |
| Guillemets français `«` `»` | `«` `»` | Conservés tels quels, jamais convertis en `"` |

### 10.3 Structure fixe imposée (indépendante du contenu du document)

Chaque chapitre est découpé en **exactement 8 blocs**, toujours dans le même ordre, avec les mêmes `id`, quel que soit le contenu réel du document source :

| # | `id` du bloc | Titre de kicker fixe | Classe(s) |
|---|---|---|---|
| 1 | `accroche` | Accroche | `block hook-block` |
| 2 | `objectifs` | Ce que tu vas apprendre | `block` |
| 3 | `concept` | Le concept expliqué simplement | `block` |
| 4 | `exemple` | Exemple concret | `block` |
| 5 | `pratique` | Comment le mettre en pratique | `block` |
| 6 | `jargon` | Le jargon de ce chapitre | `block` |
| 7 | `quiz` | Quiz — Vérifie que tu as compris | `block` |
| 8 | `suite` | Et après ? | `block` |

Chaque `## N. Titre` du document source correspond à l'un de ces 8 blocs, dans l'ordre — le titre exact du kicker est repris du document, mais l'`id`, le numéro affiché (`<span class="num">N</span>`) et le regroupement en `<article id="..." class="block">` sont fixes et ne varient jamais.

La **table des matières latérale** (`.chapter-toc`) n'est *jamais* générée à partir des sous-titres réels du chapitre : c'est toujours la même liste fixe de 8 liens (`#accroche`, `#objectifs`, `#concept`, `#exemple`, `#pratique`, `#jargon`, `#quiz`, `#suite`) avec les mêmes 8 libellés courts, à recopier à l'identique sur chaque page.

Le **header**, la **navigation mobile**, le **breadcrumb** (construit à partir du palier et du numéro de chapitre, sans le sous-titre entre parenthèses), le **footer**, et les deux `<script>` inline (surbrillance de la TOC au scroll via `IntersectionObserver`, toggle du menu hamburger) sont un **boilerplate identique** copié sur chaque page de chapitre, à l'exception des chemins relatifs et du texte du breadcrumb.

### 10.4 Règles spécifiques par bloc

**Bloc 1 — Accroche (`hook-block`)**
Le contenu du document (phrases courtes juxtaposées, liste à puces, citation) est **regroupé en 2-3 paragraphes** (`<p>`), les puces et citations étant fondues dans la prose plutôt que conservées comme listes/`<blockquote>` — mais les phrases elles-mêmes sont reprises **mot pour mot** du document, seule la mise en forme (puces → texte suivi, sauts de ligne → phrases jointes) change. Un `<h3>` est ajouté juste après le kicker : c'est la **seule reformulation acceptée de ce bloc**, une question courte rédigée pour résumer l'angle d'attaque du chapitre, à n'ajouter que si le document ne fournit déjà aucun titre à réutiliser.

**Bloc 2 — Objectifs**
`## 2. Ce que tu vas apprendre` → kicker. La phrase d'intro (`À la fin de ce chapitre, tu sauras :`) devient `<h3>` (le `:` final est supprimé). Chaque puce `* ...` devient un `<li>` de `.objectives-list`, préfixé d'un `<span class="tick">✓</span>` fixe.

**Bloc 3 — Concept**
Chaque `### Sous-titre` du document devient un `<h3>` verbatim. Les blocs de texte brut représentant un schéma, une liste de code ou une structure technique (même sans fence Markdown explicite) deviennent un `.example-card` : `<div class="example-bar">` reçoit un **nom de fichier fictif + un emoji inventés par l'éditeur** selon la nature du contenu (⚙️ pour un schéma technique, 🔗 pour une liste d'URLs, 🌐 pour du code source HTML), suivi d'un `<pre>` reprenant le contenu tel quel (les flèches `↓` du document peuvent être normalisées en `│` pour un rendu monospace plus propre).
Les citations introduites par 💡 deviennent des `.analogy-card` (fond jaune clair, bordure gauche épaisse) ; celles introduites par ⚠️ deviennent des `.pitfall` (même traitement visuel, couleur différente). Le texte de la citation est aplati en un seul paragraphe, le `:` après "Analogie" étant remplacé par un tiret cadratin ` — `.
Une liste de questions rhétoriques (citées en Markdown) devient une `.objectives-list` avec un tick différent : `<span class="tick tick-white">?</span>` (fond foncé, coche blanche) plutôt que le ✓ vert des objectifs.
Un `### Titre` d'avertissement (ex. `### ⚠️ Les pièges à éviter`) est repris verbatim en `<h3>`, et sa liste à puces devient une `.objectives-list` avec `<span class="tick">✗</span>`.

**Bloc 4 — Exemple concret**
Même logique que le bloc 3 pour les `.example-card` (nom de fichier + emoji inventés, ex. 🔗 urls.txt — seul élément systématiquement inventé de ce bloc, faute d'équivalent dans le document). Le texte des paragraphes reste repris tel quel ; les lignes courtes/citations sont seulement rejointes en phrases, sans changer les mots (même règle que le bloc 1). Si le document n'a vraiment aucun sous-titre pour ce bloc, un court `<h3>` peut être ajouté au même titre que celui de l'accroche — seulement en dernier recours. Une citation finale mettant en avant l'enjeu réel du chapitre devient une `.analogy-card`, avec un emoji et un intitulé choisis selon le sens du passage (ex. 🎯 **Le vrai problème**) ; le texte de la citation elle-même reste celui du document, seul l'habillage (emoji + label courts) est ajouté.

**Bloc 5 — Comment le mettre en pratique**
Chaque `### Étape N — Titre` devient un `.practice-step` :
```html
<div class="practice-step">
  <div class="step-num">N</div>
  <div>
    <p class="step-title">Titre (sans le préfixe « Étape N — »)</p>
    <p>paragraphe(s) repris mot pour mot ; seules les listes à puces/numérotées de cette étape sont rejointes en prose (puces → virgules), sans reformuler leur contenu</p>
  </div>
</div>
```
Un `.pitfall` n'est inséré dans une étape **que si** le document contient littéralement un passage "⚠️ Piège fréquent" à cet endroit — sinon, l'étape reste un simple paragraphe.

**Bloc 6 — Jargon**
Le `<h3>Mini-lexique</h3>` est un **intitulé fixe toujours ajouté**, même si le document source ne l'écrit pas explicitement (il passe souvent directement au tableau). Le tableau Markdown est repris selon la règle 10.2.

**Bloc 7 — Quiz**
Structure fixe systématique, quel que soit le nombre de questions du document :
- `.quiz-progress` : `Question 1/N` (N = nombre total de questions du document) + barre de progression à `0%` au chargement (la progression réelle est pilotée par `quiz.js`, pas figée dans le HTML).
- Chaque question `**Question N — Intitulé ?**` devient un `.quiz-question` avec `<p class="question-title">` reprenant l'intitulé verbatim ; toutes les questions sauf la première reçoivent l'attribut `hidden`.
- Chaque réponse `* A) Texte` devient un `.quiz-option` : la lettre (`A)`, `B)`…) est extraite dans un `<span class="letter">`, le texte de la réponse est conservé tel quel, et `data-correct="true"` est posé sur l'option correspondant à la ligne `✅ Bonne réponse : X` du document, `"false"` sur les autres.
- **Le texte explicatif de `.quiz-explain` est rédigé par l'éditeur** : le document source ne fournit souvent que la lettre de la bonne réponse (`✅ Bonne réponse : D`), sans justification. L'éditeur doit alors écrire une ou deux phrases pédagogiques qui expliquent pourquoi cette réponse est correcte, préfixées de l'emoji 💡 (remplaçant le ✅ du document) et de `<strong>Bonne réponse : X.</strong>`.
- Un bloc `.quiz-score` cause toujours en fin de quiz, avec l'attribut `hidden` : score placeholder `N/N`, une phrase de félicitations **rédigée sur mesure pour le chapitre** (référençant son sujet), un bouton `.btn-ghost` "↻ Refaire le quiz" et un bouton `.btn-primary` "Chapitre suivant →" vers `../chapitre-{N+1}/`.

**Bloc 8 — Et après ?**
Le `<h3>La suite logique</h3>` est, comme "Mini-lexique", un **intitulé fixe toujours ajouté**, non présent littéralement dans le document. Le(s) paragraphe(s) de transition sont repris mot pour mot, seuls les sauts de ligne étant regroupés en phrases suivies. La ligne finale du document (`→ **Chapitre N — Titre**`) devient un `.next-card` :
- `.next-card-prev-row` (lien "← Chapitre précédent" vers `../chapitre-{N-1}/`) — **absent** si le chapitre est le premier de son palier (voir `palier-0/chapitre-1/`, qui n'a pas cette ligne).
- `.next-card-body` avec le label fixe "Chapitre suivant", un `<h3>` reprenant le titre du prochain chapitre (préfixe `Chapitre N — ` supprimé), et un bouton `.btn-primary` "Continuer →" vers `../chapitre-{N+1}/`.

### 10.5 Métadonnées calculées, absentes du document source

Certaines informations affichées en tête de chapitre ne figurent dans **aucun** document source et doivent être déterminées à partir du contexte du site (plan du programme, position du chapitre) :

| Métadonnée | Où | Comment elle est déterminée |
|---|---|---|
| Emoji + couleur du palier (🟢🟡🔴🟣) | Breadcrumb, `.palier-tag` | Dérivé du numéro de palier selon le groupe de couleur (0-4 vert, 5-6 jaune, 7-8 rouge, 9 violet — voir 2.3) |
| `Chapitre N sur T` | `.palier-tag` | T = nombre total de chapitres du palier concerné, connu du plan global du programme, pas du document lui-même |
| `⏱️ Lecture ~X min` | `.chapter-meta` | Estimation du temps de lecture à partir de la longueur du texte du chapitre |
| `🧩 Prérequis : Chapitre N-1` / `Aucun prérequis` | `.chapter-meta` | Par convention, le chapitre précédent du même palier est le prérequis par défaut ; le premier chapitre d'un palier affiche "Aucun prérequis" |
| `✅ Quiz en fin de chapitre` | `.chapter-meta` | Texte fixe, toujours présent puisque chaque chapitre se termine par un quiz |

### 10.6 Ce qui reste à la discrétion de l'éditeur — liste exhaustive, à ne pas étendre

Conformément à la règle de reformulation minimale (10.0), **tout le reste du texte du chapitre doit être copié verbatim**. Les seuls éléments qu'il est légitime de rédiger, faute d'équivalent dans le document source, sont :
- Le `<h3>` d'accroche (question courte résumant l'angle du chapitre) — uniquement si le document ne fournit aucun titre utilisable.
- Le `<h3>` de l'exemple concret — même règle, en dernier recours seulement.
- Les noms de fichiers fictifs et emojis des `.example-bar` (ex. `⚙️ rendu.txt`) : ils n'ont structurellement aucune source possible dans un document texte.
- Les intitulés courts et emojis des `.analogy-card` quand le document ne les nomme pas déjà (le texte de la citation, lui, reste toujours celui du document).
- Les phrases de justification des `.quiz-explain`, uniquement quand le document ne donne que la lettre de la bonne réponse sans explication — si une explication existe déjà dans le document, elle doit être reprise telle quelle plutôt que réécrite.
- La phrase de félicitations du `.quiz-score`.
- Les deux `<h3>` fixes "Mini-lexique" et "La suite logique", à ajouter systématiquement même absents du document (ce sont des intitulés de gabarit, pas du contenu éditorial).

Cette liste est volontairement limitative : si un doute survient sur un passage qui n'y figure pas, la règle par défaut est de **copier le texte du document sans le modifier**, quitte à ajuster uniquement la ponctuation de jonction entre phrases fusionnées.

---

## 11. Politique de publication des chapitres non écrits

Le site est déployé tel quel sur GitHub Pages, sans étape de build ni exclusion de fichiers (`actions/upload-pages-artifact` avec `path: .`) : **tout fichier `index.html` présent dans le dépôt est accessible publiquement**, qu'il soit lié depuis une page ou non. Cela a une conséquence directe sur la gestion des chapitres pas encore rédigés :

- **Aucune page "placeholder" de chapitre ne doit exister dans le dépôt.** Tant qu'un chapitre n'a pas son contenu réel (au format décrit en section 10), son dossier `palier-P/chapitre-N/` ne doit **pas être créé**. Créer une page provisoire ("Chapitre en préparation", contenu `[Placeholder]`) revient à la publier malgré elle, puisque rien n'empêche techniquement d'y accéder directement par son URL.
- **Un chapitre non écrit est représenté uniquement par une entrée non cliquable** dans les pages qui listent le programme :
  - Dans `programme/index.html` et `palier-P/index.html` : une ligne `<div class="chapter-row disabled">…<span class="status status-draft">À venir</span></div>` (pas de balise `<a>`, pas de `href`) — convention déjà en place, à ne jamais transformer en lien avant que le chapitre existe réellement.
  - Dans un chapitre **déjà publié** qui doit annoncer le chapitre suivant (bloc "Et après ?" et bouton de fin de quiz), le CTA qui mènerait normalement vers ce chapitre doit être un **bouton HTML désactivé**, pas un lien :
    ```html
    <button type="button" class="btn btn-primary" disabled aria-disabled="true">À venir</button>
    ```
    Le titre du chapitre à venir (`<h3>` du `.next-card-body`) peut rester affiché s'il est déjà connu (annoncé dans le document source du chapitre courant) — seul le bouton de navigation doit être neutralisé, jamais transformé en `<a href>` vers une page qui n'existe pas.
- **Réactivation** : dès que le chapitre suivant est réellement rédigé et son fichier `index.html` créé (en suivant la section 10), il faut à la fois :
  1. Créer la page réelle du chapitre (jamais un fichier "placeholder" intermédiaire).
  2. Remplacer le(s) bouton(s) `disabled` par des liens `<a href="../chapitre-N/" class="btn btn-primary">` dans tous les chapitres qui y pointent en amont.
  3. Transformer la ligne `.chapter-row.disabled` correspondante en `<a class="chapter-row">` avec `<span class="status status-published">Publié</span>`, dans `programme/index.html` et `palier-P/index.html`.
  4. Mettre à jour les compteurs "X publiés" à ces deux mêmes endroits (voir 10.5).
