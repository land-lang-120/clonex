# 📘 clonex-studio — Cahier des charges

> Document rétrospectif. Source de vérité pour la vision, le périmètre et la roadmap.
> Lié à : [PROGRESS.md](PROGRESS.md) (suivi opérationnel)
> Mis à jour : **2026-04-23**

---

## 1. Vision

**CloneX Studio** est le **hub portfolio + launcher central** de toutes les apps UNIVERSAL-TECH.

Un seul site présente le studio, met en vitrine les apps livrées (jeux + outils), et permet à un visiteur de :
- Découvrir le studio en quelques secondes (positionnement studio indé games + apps mobiles)
- Tester chaque app **directement dans le navigateur** sans installer
- Installer en un clic l'app préférée comme PWA sur mobile
- Suivre les nouveautés et apps à venir

**Tagline** : « Des expériences mobiles immersives. »

**Promesse** : 100% gratuit, 100% PWA installable, 0 store, 0 friction.

---

## 2. Personas

### Persona 1 — Le visiteur curieux
- Découvre le studio via réseaux sociaux ou bouche-à-oreille
- Veut comprendre **qui est CloneX et ce qu'il fait** en 30 secondes
- Cherche un jeu sympa à essayer immédiatement (pas envie d'aller sur Play Store)
- KPI : taux de clic vers une app card

### Persona 2 — Le joueur mobile
- Cherche un jeu rapide à installer sans payer
- Apprécie l'install PWA en un clic vs. téléchargement Play Store (10 Mo+ vs. 200 Ko)
- Va revenir si l'expérience est fluide
- KPI : install PWA + temps de jeu cumulé

### Persona 3 — Le recruteur / partenaire
- Tombe sur le portfolio depuis LinkedIn / GitHub
- Évalue le sérieux : design, diversité d'apps, qualité d'exécution
- Vérifie : combien d'apps ? quelle stack ? mises à jour récentes ?
- KPI : temps passé sur about + clic sur GitHub / contact

### Persona 4 — Le futur utilisateur d'une app B2B (Pharmadroid pro, Switchr Pro)
- A entendu parler d'une app spécifique
- Arrive sur la landing page dédiée (deep link)
- Cherche à comprendre l'offre + s'inscrire
- KPI : clic vers la page dédiée + lead form (à venir)

---

## 3. Périmètre fonctionnel

### Pages livrées
| Page | Fichier | Rôle |
|---|---|---|
| Homepage portfolio | `clonex.html` | Hero + 6 apps showcase + about + footer |
| Index temporaire | `index.html` | Actuellement = jeu Tetroid intégré (vitrine playable) |
| Tetroid landing | (intégré dans `index.html`) | Jeu directement playable |
| Block Blast Royal | `block-blast-royal.html` | Landing + lien jeu |
| Bounce v4 | `bounce-v4.html` | Landing + lien jeu |
| Pharmadroid | `pharmadroid.html` | Landing + lien app |
| Sequoia | `sequoia.html` | Landing + teaser |
| Byer | `byer.html` | Landing marketplace |
| CarExpress | `carexpress.html` | Landing taxi/VTC |
| SOS | `SOS.html` | Page urgences |
| Arena prototype | `arena-prototype.html` | Démo expérimentale |
| Versus global | `versus-global.html` | Démo expérimentale |
| Select Agent | `select-agent-1.html` | Démo expérimentale |
| README PWA | manifest.json (à venir) | Install PWA du portfolio lui-même |

### Composants UI portfolio
- **Hero** plein écran avec gradient animé + badge « Studio indie actif »
- **Stats bar** : 6 apps / 12 langues / 100% gratuit / PWA installable
- **Apps grid** responsive (320px min, auto-fill)
- **App cards** avec thumbnail thématique (gradient par app), badge statut (Live/Soon/Dev), CTA Jouer/Télécharger
- **About section** présentation studio
- **Footer** avec GitHub + email contact
- **Theme toggle** dark/light persisté `localStorage.clonex_theme`
- **Toast notifications** pour feedback (PWA install, etc.)

### Apps mises en vitrine (au 2026-04-23)
| App | Catégorie | Statut sur portfolio | URL landing |
|---|---|---|---|
| Tetroid | Arcade / Puzzle | 🟢 En ligne (intégré) | `index.html` |
| Block Blast Royal | Puzzle / Stratégie | 🟠 Bientôt | `block-blast-royal.html` |
| Bounce | Arcade / Adresse | 🟠 Bientôt | `bounce-v4.html` |
| PharmaDroid | Santé | 🟠 Bientôt | `pharmadroid.html` |
| Sequoia | Productivité | 🟠 Bientôt | `sequoia.html` |
| DailyNote | Notes | 🔵 En dev | (à ajouter) |
| Byer | Marketplace | non listé | `byer.html` |
| CarExpress | VTC | non listé | `carexpress.html` |
| Switchr | Transfert P2P | non listé | (à créer) |
| Snake-Labyrinth | Arcade | non listé | (à créer) |
| Chrome-Messenger | Messagerie | non listé | (à créer) |
| SecretNote | Notes secrètes | non listé | (à créer) |

→ **5 landings manquantes** à créer : switchr, snake-labyrinth, chrome-messenger, secretnote, dailynote (en dev mais pas encore liée).

### PWA install
- `beforeinstallprompt` capturé sur la homepage
- Function `installApp(url)` redirige vers `<app>.html?install=1`
- Chaque app détecte le query param et déclenche son propre prompt PWA
- Pas de manifest.json à la racine (le portfolio lui-même n'est pas installable, seules les apps individuelles le sont)

### Serveur de dev
- `server.js` Node.js minimaliste (23 lignes, pas de dépendance npm)
- HTTP natif sur port 3000
- Sert d'abord `tetroid-pro/<url>` si existant, sinon racine
- MIME types : html/css/js/json/svg/png/jpg/ico/woff2

---

## 4. Architecture & stack

### Stack actuelle
- **HTML statique** multi-pages (pas de framework, pas de bundler)
- **CSS inline** dans chaque page (pas encore extrait)
- **JS vanilla** inline (theme toggle + PWA install)
- **Polices** : Inter + Space Grotesk (Google Fonts CDN)
- **Icônes** : emoji + SVG inline
- **Serveur dev** : Node.js HTTP natif

### Patterns
- **Mode dark/light** via `body.light` class + variables CSS scoped
- **Cards thumbnails** avec gradient distinct par app (utile pour reconnaissance visuelle)
- **Badges statut** code couleur uniforme (Live = vert, Soon = orange, Dev = gris)
- **Boutons** primary (gradient violet) + outline (border)

### Hébergement
- GitHub Pages (anciennement Netlify, liens corrigés)
- Domaine custom `clonex.studio` ou similaire (à déployer)

### Fichiers HTML existants (audit complet)
```
index.html             (681 lignes) — Tetroid game intégré (devrait être renommé tetroid.html)
clonex.html            (517 lignes) — Vraie homepage portfolio
SOS.html               — Page urgence
arena-prototype.html   — Demo expérimentale
block-blast-royal.html — Landing
bounce-v4.html         — Landing
byer.html              — Landing
carexpress.html        — Landing
pharmadroid.html       — Landing
select-agent-1.html    — Demo expérimentale
sequoia.html           — Landing
versus-global.html     — Demo expérimentale
server.js              (23 lignes) — Dev server
README.md              — Doc projet
PROGRESS.md            — Suivi
```

### Cible (post-migration Astro)
```
clonex-studio-astro/
├── src/
│   ├── pages/
│   │   ├── index.astro              # Homepage portfolio
│   │   ├── tetroid.astro
│   │   ├── byer.astro
│   │   ├── carexpress.astro
│   │   ├── pharmadroid.astro
│   │   ├── snake-labyrinth.astro
│   │   ├── switchr.astro
│   │   ├── dailynote.astro
│   │   ├── secretnote.astro
│   │   ├── sequoia.astro
│   │   ├── block-blast-royal.astro
│   │   ├── bounce.astro
│   │   ├── chrome-messenger.astro
│   │   └── 404.astro
│   ├── layouts/
│   │   ├── BaseLayout.astro         # Header + footer + meta SEO
│   │   └── AppLandingLayout.astro   # Template uniforme app
│   ├── components/
│   │   ├── AppCard.astro
│   │   ├── HeroBadge.astro
│   │   ├── StatsBar.astro
│   │   ├── ThemeToggle.astro
│   │   └── PwaInstall.astro
│   ├── content/
│   │   └── apps/                    # Collection content (1 fichier .md par app)
│   └── styles/
│       └── global.css               # Variables design system
├── public/
│   ├── icons/                       # Favicons + thumbnails OG
│   ├── robots.txt
│   ├── sitemap.xml                  # Auto-généré par Astro
│   └── manifest.json                # PWA portfolio
├── astro.config.mjs                 # SSG mode + integrations (sitemap, mdx)
├── package.json
└── tsconfig.json
```

---

## 5. Charte UI / design

### Couleurs (mode sombre)
| Token | Valeur | Usage |
|---|---|---|
| `--bg` | `#0a0a0f` | Fond principal |
| `--bg2` | `#12121a` | Sections alternées |
| `--surface` | `#1a1a26` | Cards |
| `--border` | `#2a2a3a` | Bordures + dividers |
| `--text` | `#e8e8f0` | Texte principal |
| `--text2` | `#8888a0` | Texte secondaire |
| `--accent` | `#7c3aed` | Violet primaire |
| `--accent2` | `#a855f7` | Violet clair (gradient end) |
| `--green` | `#22c55e` | Badge Live + status pulse |
| `--orange` | `#f97316` | Badge Soon |
| `--cyan` | `#06b6d4` | Gradient accents |
| `--pink` | `#ec4899` | Gradient accents |
| `--gold` | `#f5c518` | Stats numbers |

### Typographie
- **Display** : Space Grotesk 700 (logo, h1, h2, stats numbers)
- **Body** : Inter 400/600/700/900 (texte courant)
- **Letter-spacing négatif** sur titres (-1px à -2px) pour effet moderne

### Effets visuels
- **Backdrop blur 20px** sur nav fixed
- **Radial gradient** central animé sur hero
- **Card hover** : translateY(-4px) + box-shadow 12px 40px
- **Pulse animation** sur dot vert "studio actif"
- **Theme toggle** rond avec scale(1.1) au hover
- **Smooth scroll** anchor links

### Mobile
- Breakpoint 640px : nav-links cachées, stats compactes, grid 1 colonne
- Touch-friendly : padding cards > 16px, CTA pill 14×32

---

## 6. Roadmap

### v0.1 — Présent ✅
- 12 fichiers HTML statiques
- Homepage portfolio (clonex.html) avec 6 apps
- Theme dark/light persisté
- PWA install handoff vers apps individuelles
- Serveur Node.js dev

### v1.0 — Migration Astro (Q3 2026)
- [ ] Scaffold projet Astro avec TypeScript
- [ ] Migrer pages HTML en `.astro` files
- [ ] Extraire composants réutilisables (`AppCard`, `Hero`, `StatsBar`)
- [ ] Content collection pour metadata apps (1 .md par app)
- [ ] BaseLayout avec meta SEO + Open Graph + JSON-LD
- [ ] sitemap.xml + robots.txt auto-générés
- [ ] Lighthouse ≥ 95 sur toutes les pages
- [ ] PWA installable du portfolio lui-même

### v1.1 — SEO & analytics
- [ ] Meta Open Graph par page (image OG dynamique)
- [ ] JSON-LD `SoftwareApplication` par app
- [ ] Schema.org `Organization` pour CloneX Studio
- [ ] Plausible ou Firebase Analytics (privacy-friendly)
- [ ] Search Console + indexation
- [ ] Sitemap soumis Google + Bing

### v1.2 — Multilingue
- [ ] Routing i18n Astro (`/fr/`, `/en/`)
- [ ] Traduction homepage + about (FR+EN minimum)
- [ ] Hreflang tags
- [ ] Sélecteur langue persisté

### v2.0 — CMS + Blog
- [ ] Section blog (devlog, post-mortem chaque sortie d'app)
- [ ] RSS feed
- [ ] Newsletter (Buttondown ou Brevo)
- [ ] Sortie d'app = post auto

### v2.1 — Lead generation
- [ ] Form contact pour partenariat / B2B
- [ ] CRM simple (Notion API ou Airtable)
- [ ] Pages dédiées B2B (Pharmadroid Pharmacie, CarExpress Fleet, Switchr Business)

### Nice to have
- Showreel vidéo intégré sur hero
- Galerie screenshots interactive (lightbox)
- Comparateur d'apps (filtres : type, stack, statut)
- Page « presse » avec assets téléchargeables
- Page « making-of » avec stats GitHub par app

---

## 7. Risques & dépendances

### Risques techniques
- **`index.html` confus** : c'est actuellement le jeu Tetroid, pas la homepage portfolio. Visiteur arrive sur Tetroid plutôt que CloneX. À fixer en priorité.
- **5 landings manquantes** : switchr, snake-labyrinth, chrome-messenger, secretnote, dailynote (cette dernière listée en "dev" mais sans landing dédiée).
- **Aucun manifest.json** au niveau root → portfolio non-installable comme PWA (handoff vers chaque app fonctionne, mais le hub lui-même n'est pas installable).
- **Pas de système de build** : modifier 12 fichiers HTML manuellement à chaque changement de design = dette technique. Migration Astro urgente.
- **CSS inline dupliqué** : variables CSS répétées dans chaque fichier landing (incohérences possibles).
- **Pas de tests** : régression visuelle silencieuse possible.

### Risques SEO
- Pas de sitemap.xml
- Pas de robots.txt
- Pas de meta Open Graph (images non générées)
- Pas de JSON-LD schema
- Lighthouse non audité
- Pas de Search Console / Bing Webmaster Tools

### Risques business
- **Pas d'analytics** : aucune donnée sur trafic, source, conversion install
- **Pas de form contact actif** : leads partenariat perdus
- **Pas de tracking install PWA** : impossible de mesurer le funnel découverte → install
- **GitHub Pages limit** : 100 GB bandwidth/mois — OK aujourd'hui, pourrait saturer si une app devient virale

### Dépendances externes
- Google Fonts CDN (Inter + Space Grotesk) — fail si bloqué côté client
- GitHub Pages hosting
- Liens vers apps individuelles (cassent si une app est renommée/supprimée)

---

## 8. Conventions

### Naming
- Pages app : `<app-name>.html` (kebab-case)
- IDs HTML : `cx-<purpose>` ou `<scope>-<element>`
- Classes : kebab-case BEM-light (`.app-card`, `.app-thumb.tetroid`)
- Variables CSS : `--<token>` (préfixe `--accent`, `--bg`, etc.)

### Liens
- Externes : `target="_blank" rel="noopener"`
- Apps internes : relatif (`pharmadroid.html`)
- Anchor : `#apps`, `#about`, `#contact`
- PWA install : `<app>.html?install=1`

### Storage
- `clonex_theme` : `'dark' | 'light'` (persistance theme)
- Pas d'autre clé — pas de tracking visiteur

### Versioning
- Pas de versionning bundle (HTML statique = pas de cache busting nécessaire)
- À ajouter en migration Astro (hash automatique fichiers buildés)

### Déploiement
- Push sur main → GitHub Pages auto-déploie
- Pas de CI/CD pipeline (à ajouter avec migration Astro)

---

## 9. Résumé exécutif

CloneX Studio est le **hub vitrine + launcher central** des 13 apps UNIVERSAL-TECH. Stack actuelle : **HTML statique multi-pages** (12 fichiers), serveur Node.js dev minimaliste, theme dark/light, install PWA handoff vers apps individuelles. **6 apps mises en vitrine** sur la homepage `clonex.html` (Tetroid live, 5 autres "soon"), 5 apps non listées (switchr, snake-labyrinth, chrome-messenger, secretnote, dailynote sans landing dédiée). Bug actuel : `index.html` = jeu Tetroid au lieu de la homepage portfolio. **Priorité 1 : fix index.html** + ajouter les 5 landings manquantes. **Priorité 2 : migration Astro** (composants réutilisables + SEO + sitemap + manifest PWA). **Priorité 3 : analytics + form contact + tracking install PWA**.
