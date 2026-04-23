# 📊 clonex-studio — Suivi

> Voir aussi : [CAHIER-CHARGES.md](CAHIER-CHARGES.md) (vision/spec complète)
> Mis à jour : **2026-04-23**

| | |
|---|---|
| **Stack** | HTML statique multi-pages (12 fichiers) + CSS inline + JS vanilla + Node.js dev server |
| **Statut** | 🟢 Prod (contenu en place, design abouti) |
| **Type** | Hub portfolio / launcher central pour toutes les apps UNIVERSAL-TECH |
| **Tagline** | Des expériences mobiles immersives. |
| **URL** | (GitHub Pages — domaine custom à confirmer) |

---

## ✅ Fait

### Pages portfolio
- **Homepage `clonex.html`** (517 lignes) : hero gradient + stats bar + apps grid + about + footer + theme toggle
- **6 apps mises en vitrine** : Tetroid (live), Block Blast Royal, Bounce, PharmaDroid, Sequoia, DailyNote
- Cards thumbnails thématiques (gradient unique par app)
- Badges statut : 🟢 En ligne / 🟠 Bientôt / 🔵 En dev

### Landings dédiées (11 fichiers)
- `index.html` (681 lignes) — actuellement jeu Tetroid intégré (à renommer `tetroid.html`)
- `block-blast-royal.html`, `bounce-v4.html`
- `pharmadroid.html`, `sequoia.html`
- `byer.html`, `carexpress.html`
- `SOS.html` (page urgence)
- `arena-prototype.html`, `versus-global.html`, `select-agent-1.html` (démos expérimentales)

### Design system (inline)
- Variables CSS scoped : `--bg`, `--accent`, `--cyan`, `--gold` etc.
- Typographie : Inter + Space Grotesk (Google Fonts CDN)
- Mode dark/light persisté via `localStorage.clonex_theme`
- Effets : backdrop-blur nav, radial gradient hero, card hover translate, pulse animation badge

### PWA install handoff
- `beforeinstallprompt` capturé sur la homepage
- `installApp(url)` redirige vers `<app>.html?install=1`
- Chaque app détecte `?install=1` et déclenche son propre prompt

### Serveur dev
- `server.js` Node.js HTTP natif (23 lignes, 0 dépendance npm)
- Sert d'abord `tetroid-pro/<url>` si existe, sinon racine
- MIME types : 9 extensions supportées (html/css/js/json/svg/png/jpg/ico/woff2)

### Hébergement
- GitHub Pages déployé (anciens liens Netlify cassés, corrigés en 2026)
- Pas encore de domaine custom

### Documentation
- CAHIER-CHARGES.md rétrospectif (vision, personas, périmètre, architecture, roadmap)

## 🔄 En cours

- Aucun développement actif (sert le contenu existant)

## 📋 À faire (priorité décroissante)

### Critique
1. ~~Créer `CAHIER-CHARGES.md`~~ ← fait dans cette session
2. **Fix `index.html`** : actuellement = jeu Tetroid intégré, devrait être la homepage portfolio. Renommer `index.html` → `tetroid.html` et faire de `clonex.html` le nouveau `index.html` (la homepage).
3. **Ajouter les 5 landings manquantes** : `switchr.html`, `snake-labyrinth.html`, `chrome-messenger.html`, `secretnote.html`, `dailynote.html` (DailyNote est listée en "dev" sur la homepage mais sans landing dédiée).

### Important
4. **Migration vers Astro** (SSG TypeScript) :
   - Composants réutilisables (`AppCard`, `Hero`, `StatsBar`, `ThemeToggle`)
   - Content collection pour metadata apps (1 .md par app)
   - BaseLayout avec meta SEO + Open Graph + JSON-LD
   - sitemap.xml + robots.txt auto-générés
5. **SEO complet** :
   - Meta Open Graph par page (image OG dynamique)
   - JSON-LD `SoftwareApplication` par app + `Organization` pour CloneX
   - Search Console + Bing Webmaster Tools
6. **Analytics privacy-friendly** : Plausible ou Firebase Analytics
7. **Manifest PWA root** : rendre le portfolio lui-même installable
8. **Audit Lighthouse ≥ 95** sur toutes les pages

### Nice to have
9. Multilingue (FR + EN minimum) avec routing i18n Astro
10. Section blog (devlog + post-mortem chaque sortie d'app)
11. RSS feed + newsletter (Buttondown ou Brevo)
12. Form contact pour partenariats / B2B + CRM (Notion API ou Airtable)
13. Pages dédiées B2B (Pharmadroid Pharmacie, CarExpress Fleet, Switchr Business)
14. Showreel vidéo intégré sur hero
15. Galerie screenshots interactive (lightbox)
16. Comparateur d'apps (filtres : type, stack, statut)
17. Domaine custom + HTTPS configuré
