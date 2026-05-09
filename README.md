# DuoGames Design System

Design system officiel DuoGames, construit à partir du Brand Kit Canva (id `kAGyGU3K6xo`).

> **Source de vérité** : ce dépôt. Toute valeur de couleur, taille de police, espacement utilisée dans un produit DuoGames doit provenir d'ici.

## Contenu

```
duogames-design-system/
├── README.md           # Ce fichier — règles d'application + comment consommer
├── tokens.css          # Variables CSS prêtes à l'emploi (drop-in)
├── tokens.json         # Format W3C Design Tokens (Style Dictionary, Tokens Studio…)
└── brand/
    └── logo-duogames.png
```

## Identité visuelle

DuoGames a une identité **arcade / gaming / cartoon** affirmée. Trois éléments la définissent et doivent être respectés sur tous les produits :

1. **Lettrage gras à fort contour noir** — le wordmark GAMES utilise un contour noir épais sur intérieur blanc. Ce traitement peut être réutilisé sur les titres principaux et CTA majeurs (classe `.dg-heading-stroke` dans `tokens.css`).
2. **Ombre signature violet + rose** — le décalage `#695acd` + `#e7b3c3` derrière le wordmark est l'élément le plus distinctif de la marque. À réutiliser sur les éléments « héro » (titres, cards mises en avant, boutons primaires au hover). Token : `--shadow-signature`.
3. **Bleu DuoGames `#0074e6`** — couleur principale, présente sur tous les éléments structurants (CTA, accents, lettrage « DUO »).

## Palette de couleurs

### Primaires

| Token | HEX | Usage |
|---|---|---|
| `--brand-blue` | `#0074e6` | Couleur principale — « DUO », CTA, accents forts |
| `--brand-black` | `#000000` | Contours, texte principal, lettrage GAMES |
| `--brand-white` | `#ffffff` | Fonds, intérieur du lettrage GAMES |

### Secondaires

| Token | HEX | Usage |
|---|---|---|
| `--brand-gray` | `#b0b0b0` | Ombre portée gris, neutres, dividers |
| `--brand-purple` | `#695acd` | Composant de l'ombre signature |
| `--brand-pink` | `#e7b3c3` | Composant de l'ombre signature |

### Fonctionnelles (réservées à leur rôle)

| Token | HEX | Usage |
|---|---|---|
| `--brand-orange` | `#e18d00` | Avertissement, badges chauds |
| `--brand-red` | `#ba0732` | Erreur, alertes critiques |
| `--brand-green` | `#38a803` | Succès, validation |

> Les couleurs fonctionnelles sont **réservées** à leur rôle système. Ne pas les utiliser comme couleurs décoratives ou marketing.

## Typographie

**Famille unique : Poppins.** Toute la hiérarchie utilise Poppins. La hiérarchie est créée par variation de **graisse** (400, 500, 600, 700) et de **style** (regular, italic), jamais par changement de police.

### Import HTML

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;0,600;0,700;1,400;1,600&display=swap" rel="stylesheet">
```

### Échelle

| Token | Taille | Usage |
|---|---|---|
| `--text-display` | 56px | Hero, claim, accroche |
| `--text-h1` | 42px | Titre principal (référence Canva) |
| `--text-h2` | 32px | Titre secondaire |
| `--text-h3` | 24px | En-tête de section |
| `--text-h4` | 20px | Sous-titre |
| `--text-body-lg` | 18px | Corps emphasé |
| `--text-body` | 16px | Corps standard (référence Canva) |
| `--text-body-sm` | 14px | Texte secondaire |
| `--text-caption` | 12px | Légendes, mentions légales |

### Graisses

- **400 (regular)** — corps de texte
- **500 (medium)** — emphasis légère
- **600 (semibold)** — sous-titres, boutons
- **700 (bold)** — titres principaux, lettrage signature

## Comment consommer ces tokens

### En CSS pur (le plus simple)

Importer `tokens.css` une fois, puis utiliser les variables partout :

```html
<link rel="stylesheet" href="duogames-design-system/tokens.css">
```

```css
.mon-bouton {
  background: var(--brand-blue);
  color: var(--brand-white);
  font-family: var(--font-body);
  font-size: var(--text-body);
  font-weight: var(--weight-semibold);
  border: var(--stroke-base) solid var(--brand-black);
  border-radius: var(--radius-md);
  padding: var(--space-3) var(--space-6);
}
```

### En Tailwind CSS

Étendre la config Tailwind pour exposer les tokens :

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          blue:   '#0074e6',
          black:  '#000000',
          white:  '#ffffff',
          gray:   '#b0b0b0',
          purple: '#695acd',
          pink:   '#e7b3c3',
          orange: '#e18d00',
          red:    '#ba0732',
          green:  '#38a803',
        },
      },
      fontFamily: {
        sans: ['Poppins', 'system-ui', 'sans-serif'],
      },
    },
  },
};
```

### Avec Style Dictionary (export multi-plateforme)

Le fichier `tokens.json` suit le format **W3C Design Tokens**. Il est consommable par Style Dictionary, Tokens Studio (Figma plugin), ou tout outil moderne de gestion de tokens.

```bash
npm install -D style-dictionary
npx style-dictionary build --tokens tokens.json
```

### Dans Canva

Pour générer des designs Canva on-brand, passer le Brand Kit ID `kAGyGU3K6xo` au paramètre `brand_kit_id` lors de l'appel à `Canva:generate-design`. Canva applique automatiquement la palette et la typographie.

## Règles d'application

### À faire

- ✅ **Une couleur primaire par écran**. Le bleu `#0074e6` peut dominer ; les couleurs secondaires (purple, pink) restent dans les ombres signatures et accents ponctuels.
- ✅ **Contour noir épais** sur les éléments à fort impact (titres, CTA principaux). C'est l'identité de la marque.
- ✅ **Ombre signature violet+rose** sur les éléments « héro ». La reproduire au pixel près (4px+8px de décalage, ou 2px+4px en version douce).
- ✅ **Poppins partout**. Hiérarchie par graisse, jamais par police.
- ✅ **Couleurs fonctionnelles réservées** à leur rôle système (ne pas utiliser le rouge `#ba0732` pour un titre marketing, etc.).
- ✅ **Contraste WCAG AA minimum** sur tous les textes (ratio 4.5:1 pour le corps, 3:1 pour les titres ≥ 18px bold).

### À ne pas faire

- ❌ Mélanger Poppins avec une autre police de display (Fraunces, Inter, Roboto, etc.).
- ❌ Inventer des nuances « entre deux tokens » (par ex. un bleu plus clair que `#0074e6`). Si une variante manque, l'ajouter au design system d'abord.
- ❌ Utiliser le violet `#695acd` ou le rose `#e7b3c3` comme fonds pleins ou couleurs de texte primaires — ils sont conçus pour les ombres signatures.
- ❌ Empiler plusieurs ombres sur un même élément (signature ET shadow-md). Choisir une seule signature visuelle par élément.
- ❌ Utiliser des hex en dur dans le code produit. Toujours passer par les tokens.

## Tokens « à valider »

Les sections suivantes ne sont **pas** spécifiées dans le Brand Kit Canva original mais sont nécessaires en pratique. Les valeurs proposées sont des défauts conservateurs cohérents avec l'identité visuelle. **À valider** avec une charte étendue ou avec un designer si DuoGames en mandate un :

- Échelle d'espacement (`--space-1` à `--space-24`)
- Rayons de bordure (`--radius-sm` à `--radius-pill`)
- Épaisseurs de contour (`--stroke-thin` à `--stroke-heavy`)
- Ombres standard non-signature (`--shadow-sm/md/lg`)
- Transitions (`--transition-fast/base/slow`)

## Versionning

Ce design system suit le **versionning sémantique** :

- **MAJOR** (`1.x.x` → `2.x.x`) — Changement cassant : suppression d'un token, renommage, changement majeur de palette.
- **MINOR** (`x.1.x` → `x.2.x`) — Ajout de tokens, nouvelle échelle. Rétrocompatible.
- **PATCH** (`x.x.1` → `x.x.2`) — Correction de valeur, ajustement mineur.

Tout changement passe par une PR avec :
1. Description du changement
2. Capture avant/après
3. Liste des produits potentiellement impactés (ExcelQuest, CRM, DiagErgo, site)

## Pour les contributeurs Claude / Claude Code

Quand tu travailles sur un produit DuoGames qui consomme ce design system :

1. **Lire ce README** avant tout brief design.
2. **Charger `tokens.css`** dans le projet. Ne jamais dupliquer les valeurs.
3. **Refuser** une demande qui contredit la charte (ex : « mets-moi un titre en Inter »). Proposer l'alternative conforme.
4. **Signaler** quand un design demande un token absent du système (ex : un bleu plus foncé que `#0074e6`). Soit on l'ajoute proprement au design system, soit on trouve une alternative avec les tokens existants.

---

**Version 1.0.0** — Mai 2026 — Brand Kit source : `kAGyGU3K6xo`
