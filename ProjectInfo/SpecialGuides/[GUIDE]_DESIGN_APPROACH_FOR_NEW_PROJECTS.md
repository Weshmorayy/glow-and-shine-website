# Guide : Approche Design pour Nouveaux Projets Clients

Ce guide documente la méthode concrète pour concevoir des sites web clients qui sont **vraiment uniques, adaptés au métier, et visuellement distincts** — à l'opposé du "AI slop" générique.

Écrit après le projet Lunettes de Paris (redesign complet suite au rejet du premier design).

---

## 1. 🧠 Avant d'écrire une seule ligne de code

### Étape 1 — Étudier le métier réel du client
Demande-toi : **quel site web ferait un professionnel de CE métier, pas un webmaster généraliste ?**

| Métier | Ce que le site doit faire avant tout |
|--------|--------------------------------------|
| Opticien | Montrer les produits comme une boutique de mode. Examen de vue = service médical à valoriser. Guide morpho = outil de conversion. |
| Pâtisserie | Vitrine appétissante. Tarifs précis à la part. Commande WhatsApp rapide. Saveurs listées. |
| Parfumeur en gros | Catalogue searchable. Prix au volume. Olfactory families. Commande professionnelle. |
| Architecte d'intérieur | Portfolio immersif. Projets = héros visuels. Pas de text wall. |
| Bijouterie | Produits sur fond neutre. Matériaux précis. Tailles/poids. Confiance = artisanat mis en avant. |

**Règle d'or** : Le site doit ressembler aux meilleurs sites du secteur mondial — pas à un template généraliste.

### Étape 2 — Identifier 3 références sectorielles de haut niveau
Avant de coder, ouvre les sites des leaders mondiaux du secteur et note :
- Quelle est leur structure de navigation ?
- Comment présentent-ils leurs produits/services ?
- Quel est leur rythme typographique ?
- Quelle est leur palette couleur et leur usage des espaces blancs ?

**Exemples pour secteurs courants :**
- Opticien → Warby Parker, Ray-Ban, AHLEM Paris, Mykita
- Parfumerie → Fragrantica, Maison Margiela Fragrances, Aesop
- Pâtisserie → Ladurée, Pierre Hermé Paris
- Bijouterie → Mejuri, Catbird NYC
- Médical → Mayo Clinic, Cleveland Clinic (minimalisme fonctionnel)

### Étape 3 — Analyser la présence sociale du client
Le Facebook/Instagram du client EST le brief design. Extraire :
- **Palette couleur réelle** (depuis le logo et les visuels de posts)
- **Style typographique** des posts (bold caps ? script ? mixte ?)
- **Format des images** (plein cadre ? produit isolé ? lifestyle ?)
- **Ton du texte** (formel ? proximité ? humour ?)
- **Accroches récurrentes** → deviennent les slogans du site

---

## 2. 🏗️ Architecture de page : penser sections, pas composants

### Le piège du "composant générique"
L'erreur classique : assembler des composants React réutilisables sans réfléchir à leur pertinence pour le métier.

```
❌ Mauvaise approche (AI template) :
Hero standard → 3 Feature Cards → Pricing Grid → Testimonials → CTA → Footer

✅ Bonne approche (Lunettes de Paris) :
Hero cinématique plein écran (photo lifestyle) 
→ Marquee marques en stock
→ Catalogue scroll horizontal (les produits SONT le site)
→ Split éditorial asymétrique (accroche visagisme)
→ Guide morpho interactif (outil métier unique)
→ Services numérotés (01/02/03/04 — pas d'icônes génériques)
→ Assurances (spécificité métier = confiance immédiate)
→ Booking split (photo + form minimaliste)
→ Centres (2 adresses réelles, liens directs)
```

### Règles de rythme visuel
1. **Alterner fond clair / fond sombre** entre les sections. Jamais 3 sections blanches d'affilée.
2. **Varier la densité** : section pleine (catalogue) → section aérée (assurances minimaliste).
3. **Au moins une section plein viewport** par page (hero, split éditorial, ou image de fond).
4. **Typographie contrastée** : grand titre serif + petit corps sans-serif. Ne jamais utiliser la même taille partout.

---

## 3. 🎨 Palette & Typographie : extraire, ne pas inventer

### Extraire la palette du client
**Méthode concrète :**
1. Ouvrir le logo PNG dans un éditeur
2. Utiliser un color picker sur les couleurs dominantes
3. Définir exactement : couleur principale, couleur accent, couleur CTA

**Ne jamais** choisir une palette "qui va bien" en général. Toujours partir du logo réel.

**Exemple — Lunettes de Paris :**
- Logo analysé → `#0A1931` (navy profond), `#D90429` (rouge tour Eiffel), `#FFB703` (jaune badge)
- Ces 3 couleurs + blanc = tout le site. Aucune autre couleur inventée.

### Typographie éditoriale sans dépendances
Pour un rendu haut de gamme sans Google Fonts ni web fonts :
```css
/* Titres éditoriaux — fonctionnent partout */
.font-serif {
  font-family: Georgia, 'Times New Roman', Times, serif;
}

/* Corps — ultra-lisible, natif */
body {
  font-family: system-ui, -apple-system, 'Segoe UI', sans-serif;
}
```

**Usage :**
- `font-serif` : H1, H2, citations, noms de produits premium
- `system-ui` : corps de texte, labels, boutons, prix

---

## 4. 🧩 Composants : les patterns qui fonctionnent

### Hero — Plein viewport cinématique
```tsx
// ✅ Toujours utiliser une vraie image éditoriale en background
<section
  className="min-h-screen bg-cover bg-center relative flex items-end"
  style={{ backgroundImage: "url('/images/editorial/hero.jpg')" }}
>
  <div className="absolute inset-0 bg-gradient-to-t from-black/75 via-black/25 to-transparent" />
  
  {/* Contenu positionné en bas-gauche */}
  <div className="relative z-10 px-6 md:px-16 pb-20 max-w-3xl">
    <h1 className="font-serif text-white text-5xl md:text-7xl leading-tight mb-6">
      Titre principal<br />en deux lignes.
    </h1>
    {/* CTAs — jamais plus de 2 */}
    <a href="#action" className="bg-[#D90429] text-white px-8 py-4 ...">CTA Principal →</a>
    <a href="#catalogue" className="border border-white text-white px-8 py-4 ...">CTA Secondaire</a>
  </div>
</section>
```

### Produits — Rail scroll horizontal
```tsx
// ✅ Badge HORS du overflow-hidden — règle critique
<div className="min-w-[280px] flex-shrink-0 bg-white">
  {/* Badge en dehors — jamais clippé */}
  <div className="bg-[#0A1931] text-white text-xs px-3 py-1.5 inline-block">
    {badge}
  </div>
  {/* Image isolée dans son propre overflow-hidden */}
  <div className="overflow-hidden h-[220px] flex items-center justify-center">
    <img src={image} className="h-full w-full object-contain" />
  </div>
  {/* Info produit */}
  <div className="py-5">
    <p className="text-xs uppercase tracking-widest text-gray-400">{brand}</p>
    <h3 className="font-serif text-xl mt-1">{name}</h3>
    <p className="font-bold mt-3">{price}</p>
  </div>
</div>
```

### Services — Liste numérotée (pas d'icônes)
```tsx
// ✅ Numéros en rouge + dividers = professionnel
// ❌ Jamais : icône dans un rond + titre + texte + card border
<div className="divide-y divide-white/10">
  {services.map((s, i) => (
    <div className="flex gap-8 py-10">
      <span className="font-serif text-[#D90429] text-4xl font-bold">
        {String(i+1).padStart(2, '0')}
      </span>
      <div>
        <h3 className="text-white font-bold text-xl uppercase">{s.title}</h3>
        <p className="text-white/50 text-sm mt-2">{s.description}</p>
      </div>
    </div>
  ))}
</div>
```

### Navigation — Transparente scroll-aware
```tsx
// ✅ Transparente sur hero → blanche au scroll
// ❌ Jamais une barre d'adresse collée au-dessus de la nav
const [scrolled, setScrolled] = useState(false);
useEffect(() => {
  const onScroll = () => setScrolled(window.scrollY > 60);
  window.addEventListener('scroll', onScroll, { passive: true });
  return () => window.removeEventListener('scroll', onScroll);
}, []);

<header className={`fixed top-0 z-50 transition-all duration-300 ${
  scrolled ? 'bg-white border-b shadow-sm' : 'bg-transparent'
}`}>
```

---

## 5. 📸 Images : règles strictes

### Images produits
- **Toujours sur fond blanc pur `#FFFFFF`** — utiliser des PNGs avec fond retiré
- `object-contain` dans un container fixe — jamais `object-cover` pour les produits
- Fond du container = `bg-white` — jamais gris ou transparent sur fond coloré
- Les badges/labels se positionnent **EN DEHORS** du `overflow-hidden`

### Images éditoriales (hero, split)
- `object-cover` + `position: absolute inset-0` pour remplir totalement
- Toujours ajouter un gradient overlay pour la lisibilité du texte
- Utiliser les vraies photos du client en priorité (stock photos en fallback)
- **Jamais** utiliser de screenshots de réseaux sociaux directement dans le site

### Organisation dans `/public/images/`
```
/public/images/
  brand/          → logo.png, favicon, og-image
  products/       → PNGs fond blanc uniquement
  editorial/      → photos lifestyle, héros, splits
  optimized/      → versions WebP/AVIF compressées
```

---

## 6. ✍️ Copywriting : réel et précis

### Les 4 règles
1. **Prix exacts** → "65 000 FCFA" pas "prix compétitifs"
2. **Lieux réels** → "Plateau, Ave Chardy" pas "centre-ville d'Abidjan"
3. **Délais concrets** → "Bilan visuel en 15 min" pas "rapide et efficace"
4. **Termes du métier** → "verres progressifs Essilor", "acétate 8mm biseauté main"

### Slogans : toujours depuis les posts sociaux du client
Ne jamais inventer un slogan. Le chercher dans :
- Les légendes Facebook/Instagram récurrentes
- Les accroches des visuels publicitaires
- Les expressions orales de l'équipe (recueillies au brief)

---

## 7. 🚀 Checklist finale avant livraison

- [ ] La page ressemble-t-elle aux meilleurs sites du secteur ? (montrer une capture à quelqu'un sans contexte)
- [ ] Peut-on deviner le métier du client en 3 secondes sans lire le texte ?
- [ ] Les sections ont-elles des rythmes visuels variés ? (dense / aéré / image / texte)
- [ ] Zéro card avec `rounded-2xl border` répété partout ?
- [ ] Les badges produits sont-ils hors du `overflow-hidden` ?
- [ ] La palette vient-elle du logo réel du client ?
- [ ] Les prix sont-ils en FCFA réels (pas génériques) ?
- [ ] La nav est-elle transparente sur le hero ?
- [ ] Les produits ont-ils des images fond blanc propres (PNG) ?
- [ ] Zéro mention "Weshmorayy" ou agence dans le footer ?
- [ ] Le build TypeScript passe sans erreur ?
- [ ] Pushé sur GitHub avec URL clickable ?
