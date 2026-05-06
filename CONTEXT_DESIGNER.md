# CONTEXT — OpSee Pitch Deck — Animation Pass

> **Pour l'IA qui prend la suite.** Ce fichier est ton brief complet. Lis-le en entier avant d'écrire la moindre ligne de code. Il contient tout ce qu'il faut pour comprendre OpSee, le pitch, le code en place, et — surtout — **ce que tu as le droit (et pas le droit) de faire**.

---

## 0. TA MISSION EN UNE PHRASE

**Transformer ce pitch deck (déjà solide sur le fond) en une expérience visuelle de niveau keynote Apple, en y ajoutant des animations riches et chorégraphiées — sans jamais toucher aux mots ni à leur formulation. Tu peux changer *comment* le texte est présenté visuellement (layout, hiérarchie, découpage en blocs), mais pas *ce qui est dit*.**

### Le principe en une ligne

> **Le fond (mots, formulation, ce qui est dit) ne change pas. La forme (layout, animations, hiérarchie visuelle) peut tout changer.**

---

## 1. ⛔ RÈGLES ABSOLUES — À LIRE EN PREMIER

Ces règles ne sont pas négociables. Si tu hésites, **ne touche pas**.

### ❌ INTERDICTIONS STRICTES (sur le contenu textuel)

1. **Ne modifie AUCUN mot.** Pas un mot, pas une virgule, pas un accent, pas une majuscule. Le contenu a été itéré, validé, mémorisé par le présentateur. Chaque mot reste **bit-perfect**.
2. **N'ajoute AUCUN mot.** Pas de nouvelle phrase, pas de nouveau bullet, pas de nouveau label, pas de nouveau pill, pas de nouvelle citation, pas de nouvelle slide.
3. **Ne supprime AUCUN mot.** Pas de phrase coupée, pas de stat retirée, pas de slide masquée.
4. **L'ordre des slides est figé.** Tu ne réorganises pas la séquence narrative globale.
5. **Ne touche pas aux slides S1 (gauge 67%) ni S1B (MES explainer).** Elles sont déjà au niveau attendu et servent de référence stylistique. Tu peux **lire** leur code pour comprendre le ton, mais pas le modifier.
6. **N'introduis aucune nouvelle dépendance** (pas de Lottie, pas de Three.js, pas de Framer Motion, pas de bibliothèque tierce). GSAP + plugins déjà chargés = ta seule boîte à outils JS.
7. **Pas de son.** `sound.js` a été retiré volontairement. Les `if(window.OPSEE_SOUND)` peuvent rester (no-op), mais ne réintroduis aucun audio.

### ✅ CE QUE TU AS LE DROIT DE FAIRE

1. **Animer.** Massivement. C'est l'objectif principal.
2. **Réorganiser visuellement le contenu d'une slide** — tant que **le nombre de mots et le sens sont préservés**. Concrètement, tu peux :
   - **Splitter** un bloc de texte en deux blocs (ex : un paragraphe → un titre + un sous-titre, ou une longue phrase → 2 bulles distinctes)
   - **Regrouper** deux éléments en un
   - **Déplacer** un élément (gauche → droite, haut → bas)
   - **Changer la hiérarchie visuelle** (un mot qui devient un highlight, une stat qui devient le focus principal, un bullet qui devient une card)
   - **Recomposer le layout** (1 colonne → 2 colonnes, grid → stack, etc.)
   - **Découper différemment les `<br>`** (changer où se coupent les lignes)
   - **Re-balancer les emphases** (`<strong>`, `<em>`, gradients)

   👉 **Test à faire** : si tu copies tout le texte rendu de la slide AVANT et APRÈS ta modif, tu dois obtenir **exactement les mêmes mots dans le même ordre logique**. Aucun mot ajouté, aucun mot retiré, aucune reformulation.

3. **Ajuster les styles CSS** (couleurs dans la palette existante, transforms, glows, depth, blur, gradients, sizes, spacings) pour servir l'animation et la composition.
4. **Ajouter des éléments décoratifs purs** (SVG paths, particules, traînées lumineuses, lignes de fond, glow auras, formes géométriques, icônes décoratives) qui ne portent **aucun contenu informatif** — ils enrichissent le visuel sans s'ajouter au discours.
5. **Réorganiser/refactorer le code JS d'animation** pour rendre les chorégraphies plus propres.
6. **Améliorer les transitions inter-slides** (le shape-overlay actuel est fonctionnel mais peu mémorable).
7. **Créer des fonctions `animateSX(s)`** custom par slide, sur le modèle de `animateS1` qui existe déjà.

### 📏 RÈGLE D'OR

**Le contenu textuel d'une slide, lu à voix haute APRÈS ton travail, doit être identique à celui d'AVANT — mêmes mots, même ordre, même sens.** Tu peux changer comment c'est *montré* (layout, hiérarchie, animation, découpage en blocs), mais pas *ce qui est dit*.

Le présentateur connaît son texte par cœur. Il doit pouvoir reprendre le deck après ton travail et présenter sans se réadapter au discours. Seul le ressenti visuel doit avoir changé — passé de "joli" à "wow".

---

## 2. CE QU'EST OPSEE (contexte produit)

### Le problème qu'OpSee résout

Un **MES** (Manufacturing Execution System) est la "tour de contrôle" d'une usine industrielle. Il pilote la production en temps réel : suivi des machines, calcul de l'OEE (Overall Equipment Effectiveness), historique des arrêts, ordres de fabrication, traçabilité.

**Aujourd'hui, le marché du MES est verrouillé par 3-4 géants** : Siemens Opcenter, SAP DMC, Rockwell FactoryTalk. Leurs solutions coûtent **500k€ à 3M€ par site**, prennent **18 à 36 mois à déployer**, et créent un **vendor lock-in** total.

**Résultat** : 67% des PME européennes ont un niveau bas ou très bas de digitalisation industrielle. Elles gèrent leur usine avec Excel, du papier, ou rien. Elles n'ont structurellement pas accès au MES, alors qu'elles représentent **99,8% des entreprises EU**.

### La solution OpSee

**OpSee = le premier MES open source pensé pour les PME industrielles.**

- **Open source** : code auditable, pas de vendor lock-in, auto-hébergeable
- **Modulaire** : tu paies uniquement les modules dont tu as besoin
- **Offline-first** : tourne sur un mini-PC dans l'usine, fonctionne sans internet
- **IA intégrée** : chatbot qui interroge les données de production en langage naturel ("Quel équipement a eu le plus d'arrêts cette semaine ?")
- **Conforme ISA-95 / ISA-88** : standards industriels, interopérable avec les ERP existants
- **Made in Belgium** : RGPD natif, support local, écosystème AgiNtech

### Modèle économique

Freemium type **Odoo**, appliqué au MES :

| Plan | Prix | Cible |
|------|------|-------|
| **Open Source** | Gratuit, toujours | Auto-hébergement, code complet |
| **Premium** | 59 €/mois/équipement | Modules avancés (IA, ERP, lots), connecteurs industriels |
| **Enterprise** | 95 €/mois/équipement | Tout Premium + support + installation clé en main |

### État du projet

- **8 mois** de développement
- **5 early adopters** signés
- **Premier déploiement commercial** : juin 2026
- Marché total : **$16 Mds** (2025), CAGR **12%/an**, **160k+ PME industrielles cibles** sur BE/FR/DE/AT/CH

### L'équipe

**4 cofondateurs** (étudiants/jeunes diplômés) :
- **Adam Bernard** — Frontend / UX
- **Nathan Moreau** — Backend / Architecture
- **Juliette Marchand** — Commercial / Stratégie
- **Louis Verbeeren** — Finance / Juridique

**Incubés par AgiNtech** (intégrateur industriel belge, 20+ ans d'expérience) :
- **Christophe Camerlynck** — CEO AgiNtech, mentor
- **Peter Mees** — Expert MES, mentor

### Tagline

> **Open · Smart · Scalable**
> *Turn complexity into clarity.*

---

## 3. LE PITCH (contexte événement)

| Paramètre | Valeur |
|-----------|--------|
| **Événement** | CBC Pitch Challenge 2026 |
| **Lieu** | Bruxelles, Belgique |
| **Format** | 5 minutes de pitch + Q&A |
| **Audience** | 4 personnes (jury intime, pas une grande salle) |
| **Date** | Mercredi 13 mai 2026 |
| **Langue** | Français |
| **Tonalité visée** | Premium, épuré, "keynote Apple", riche en animations chorégraphiées |

**Ce que l'audience doit ressentir** : "Ils ont passé combien de temps là-dessus ? On dirait une vraie boîte." → Le deck doit être un **signal de sérieux et de craft**, en lui-même un argument que l'équipe est capable de livrer un produit fini.

---

## 4. STACK TECHNIQUE (ce que tu trouveras dans le code)

### Fichier principal

**`index.html`** — un seul fichier monolithique (~1180 lignes) :
- HTML structurel
- CSS inline (entre `<style>` au début)
- JS inline (entre `<script>` à la fin)
- Toutes les images dans `img/`

### Sections clés du fichier (repères)

| Lignes | Contenu |
|-------|---------|
| 10-19 | Variables CSS (palette, fonts) |
| 23-87 | **Tuning panel** — overrides per-slide (margins, sizes). Si tu ajustes du positioning, c'est ici. |
| 89-310 | Styles globaux (cards, pills, tags, stats, etc.) |
| 311-450 | Styles per-slide |
| 455-655 | Markup des slides (s0, s1, s1b, s2, s3, s4, s5, s7, s8, s9, s10, s12, s13) |
| 657-755 | Slides backup (Q&A jury) |
| 765-770 | `gsap.registerPlugin(...)` |
| 793-869 | **`animateS1()`** — référence d'orchestration custom (gauge keynote) |
| 870-905 | Particles canvas + orb mouse-follow |
| 909-960 | Transition shape-overlay inter-slides |
| 967-1050 | **`hideSlide()` / `freezeContents()`** — reset state pour replay |
| 1048-1180 | Handlers des `data-a="..."` (animation génériques) |

### Plugins GSAP déjà chargés

```js
gsap.registerPlugin(DrawSVGPlugin, ScrambleTextPlugin, MotionPathPlugin /*, ScrollTrigger, SplitText, Flip, CustomEase */);
```

Vérifie en haut du `<script>` quels sont exactement importés. Si tu en as besoin d'un autre du club GSAP, **importe-le via la CDN GSAP officielle** (les autres sont déjà inclus dans `GSAP/` localement).

### Système d'animation générique : `data-a="..."`

Chaque élément avec un attribut `data-a` est animé automatiquement à l'entrée de sa slide :

| `data-a=` | Comportement |
|-----------|--------------|
| `lines` | Split par `<br>`, reveal y de 110%→0% avec stagger 0.11s |
| `fade` | Opacity 0→1 + y 25→0, stagger 0.06s |
| `scale` | Scale 0.5→1 + rotateX 12→0, ease back.out(1.5), stagger 0.1s |
| `stagger` | Enfants : scale 0.96→1 + y 28→0, stagger 0.07s |
| `grid` | Enfants shuffled : scale 0.92→1 + rotateX 12→0, stagger 0.08s |
| `counter` | Tween `v: 0 → data-count`, durée 1.6s, écrit en live `Math.round(v) + data-suffix` |
| `scramble` | ScrambleText vers `data-text`, reveal 0.3s, speed 0.4 |
| `rolling` | Boucle verticale de `<span>` enfants (pour le closing) |
| `mes-stack` | Custom S1B (tiers + flow-dots) |

**À toi de décider**, slide par slide, si :
- Le `data-a` générique suffit (tu peux le garder ou le remplacer par mieux)
- Tu construis une **`animateSX(s)`** custom (modèle : `animateS1`)

### Pattern d'orchestration custom (référence : `animateS1`)

Voici le squelette à reproduire pour les slides "wow" :

```js
function animateSX(s){
  // 1. Récupérer les éléments
  const a = s.querySelector('.element-a');
  const b = s.querySelectorAll('.elements-b');

  // 2. RESET (état initial avant l'anim)
  gsap.set(a, {opacity:0, y:30, scale:.9});
  gsap.set(b, {opacity:0, y:20});

  // 3. Chorégraphie (delays explicites pour contrôler le timing global)
  gsap.to(a, {opacity:1, y:0, scale:1, duration:.8, ease:'power3.out', delay:.2});
  gsap.to(b, {opacity:1, y:0, duration:.6, ease:'power3.out', stagger:.08, delay:.5});

  // 4. (optionnel) Moments d'impact, pulses, glows
  gsap.delayedCall(1.4, () => {
    gsap.fromTo(a, {scale:1}, {scale:1.05, duration:.2, yoyo:true, repeat:1});
  });
}
```

Puis :
- Appeler `animateSX(s)` dans la fonction d'entrée de slide (cherche le switch ou le `if(s.id==='sX')` autour de la ligne où `animateS1` est appelée)
- Ajouter le **reset symétrique** dans `freezeContents()` (sinon flash au retour)

### Reset / replay (CRITIQUE)

Quand on quitte une slide et qu'on y revient, l'animation doit **rejouer depuis zéro**. Le pattern :

```js
function freezeContents(s){
  if(s.id === 'sX'){
    // Remettre tous les éléments animés dans leur état initial,
    // identique au RESET de animateSX
    const a = s.querySelector('.element-a');
    if(a) gsap.set(a, {opacity:0, y:30, scale:.9});
    // ...
  }
  // Le reste (data-a génériques) est déjà géré plus bas dans la fonction
}
```

**Si tu oublies ce reset, tu auras un flash visuel au retour sur la slide.**

### Palette / tokens visuels

```css
--purple:        #8E33FF;  /* principal */
--purple-light:  #A855F7;  /* accents */
--purple-dark:   #7928CA;  /* dégradés foncés */
--purple-glow:   rgba(142,51,255,.25);
--bg:            #F9FAFB;  /* fond principal (blanc cassé) */
--bg2:           #F4F6F8;
--surface:       #FFFFFF;  /* cartes */
--surface2:      rgba(142,51,255,.06);
--border:        rgba(142,51,255,.18);
--border-light:  rgba(0,0,0,.08);
--text:          #1C252E;
--text-muted:    rgba(28,37,46,.5);
--green:         #22C55E;
--amber:         #F59E0B;
```

**N'introduis aucune nouvelle couleur.** Tout doit rester dans cette gamme violet/blanc/sombre. Si tu as besoin d'un effet, joue sur l'opacité, le glow, ou le gradient.

### Typographie

- **Outfit** (200-900) — corps, titres
- **Space Mono** (400, 700) — tags uniquement (en haut de chaque slide)

### Backgrounds globaux

- **2 glow-orbs** flous (radial gradient, blur 120px) qui suivent légèrement la souris
- **Grain SVG fractal** fixed, opacity 0.025
- **Particles canvas** (45 points reliés par lignes courtes)
- Sur `#s1` uniquement : pulse radial supplémentaire (`@keyframes s1Pulse`)

---

## 5. SLIDE PAR SLIDE — CONTENU EXACT (À PRÉSERVER)

> **Lis-toi cette section comme un oracle.** Chaque caractère ci-dessous est dans le fichier et doit y rester. Tu peux ajouter du visuel autour, **jamais modifier ce qui est entre guillemets**.

### S0 — Standby

Écran d'attente avant le pitch. Vidéo / logo statique. Pas de contenu textuel critique.

**Tâche d'animation** : optionnel — peut rester minimal (l'écran de standby tourne avant que la salle soit prête).

---

### S1 — Accroche ⭐ (RÉFÉRENCE — NE PAS TOUCHER)

**Tag** : `CBC Pitch Challenge 2026`

**Contenu** : Gauge SVG animée centrée. Au centre : `67%`. En dessous :
> des **PME européennes**
> ont un niveau **bas ou très bas** de digitalisation.
> Elles gèrent leur usine avec **Excel, du papier, ou rien**.

**Animations en place** : ring frames stagger → ticks sweep → number blur-to-sharp → progress ring fill 0→67% sync avec counter → pulse impact + glow. Subtitle + hook reveal en sync avec le fill (delay 1.6s).

**👉 Cette slide est la référence du niveau de craft attendu sur les autres slides "wow".**

---

### S1B — Pause pédagogique ⭐ (RÉFÉRENCE — NE PAS TOUCHER)

**Tag** : `30 secondes pour comprendre`

**Contenu** :
- Titre : `C'est quoi un MES ?`
- Subtitle : `La tour de contrôle de l'usine.`
- Stack à 3 niveaux :
  - **ERP** — Vend & planifie
  - **★ MES** — Pilote
  - **MACHINES** — Produisent
- Punchline : `Sans MES, l'usine vole à l'aveugle.`

**Animations en place** : tiers fade up/down + flow-dots animées qui circulent verticalement entre les 3 niveaux en boucle.

---

### S2 — Le Problème

**Tag** : `Le problème`

**Titre** : `Le MES est réservé\naux grands` (avec `aux grands` en italic accent)

**Subtitle** : `Les PME représentent **99.8%** des entreprises EU — mais n'ont pas accès au MES.`

**3 stat-cards** :
| # | Num | Label |
|---|-----|-------|
| 1 | `500 k€+` | Investissement initial MES Siemens / SAP |
| 2 | `18 mois` | Durée d'intégration moyenne |
| 3 | (icône cadenas) | Verrouillage chez un seul éditeur |

**État anim actuel** : counters tournent, cards entrent en stagger, puis figées.

**🎯 Animation à enrichir** : faire ressentir la **douleur**. Idées : zoom progressif sur les chiffres, tremor subtil, cadenas qui se ferme avec un "click" visuel et un éclat lumineux, ombre qui s'assombrit, le subtitle qui rentre comme un coup de marteau.

---

### S3 — La Solution

**Tag** : `Notre solution`

**Titre** : `Le premier MES\nopen source et accessible`

**Subtitle** : `**MES de grand compte. Prix de PME.**`

**3 pills** :
1. (icône cadenas ouvert) Open Source
2. (icône grid) Modulaire
3. (icône wifi-off) Sans internet

**État anim actuel** : stagger basique, très plat.

**🎯 Animation à enrichir** : transition contrastée avec S2 (douleur → libération). Les pills méritent un traitement plus iconique : draw SVG des icônes, lift hover-like, glow d'apparition, peut-être qu'elles s'assemblent depuis 3 directions.

---

### S4 — Le Produit ⭐ PRIORITÉ #1

**Tag** : `Le produit`

**Titre** : `Ce n'est pas un prototype.\nC'est un produit.`

**Grid 2×2** de 4 screenshots :
| Image | Label |
|-------|-------|
| `img/cockpit.png` | Cockpit personnalisable — 39 widgets |
| `img/OEE.png` | Productivité temps réel (OEE) |
| `img/timeline.png` | Historique des arrêts machines |
| `img/Arbre_equipment.png` | Gestion équipements (normes ISA-95/88) |

**État anim actuel** : entrée stagger basique. Énorme potentiel raté.

**🎯 Animation à enrichir — TRAVAIL PRINCIPAL** :
C'est LA slide où on prouve que le produit existe. Idées combinables :
- Reveal séquentiel cinématique (chaque image entre individuellement avec un beat)
- Parallax / depth subtil entre image et label
- Sur survol ou un beat dédié, **focus zoom** sur un détail (un widget, un graphe, une stat numérique dans le screenshot)
- Effet "stack de cartes" qui se déploient
- Glow autour de la carte active
- Possibilité d'un **mini moment "feature spotlight"** : une carte se met en avant 2s, montre ses chiffres, puis revient au grid
- Light sweep / shine effect sur les bords

Cette slide est **celle qui doit le plus impressionner**.

---

### S5 — L'IA

**Tag** : `IA intégrée`

**Titre** : `Parlez\nà votre usine.`

**Layout deux colonnes** :
- **Gauche (texte)** :
  - Quote : `"Quel équipement a eu le plus d'arrêts cette semaine ?"`
  - `→ Réponse instantanée, avec données temps réel.`
  - Description : `Chatbot IA intégré, capable d'interroger les données de production en **langage naturel**.`
- **Droite (image)** : `img/chatbot.jpeg`

**État anim actuel** : texte stagger + image scale.

**🎯 Animation à enrichir** : faire **vivre le dialogue**.
- La quote tapée en **typewriter** (ScrambleText ou char-by-char) avec curseur clignotant
- La flèche `→` qui se draw en SVG
- L'écran chatbot répond avec un délai (comme s'il calculait), peut-être avec un dot-loader animé d'abord, puis le texte de réponse qui apparaît
- Glow pulse sur le mot "langage naturel"
- Particules qui circulent du texte vers l'écran (visualisation de la requête envoyée)

---

### S7 — Le Marché

**Tag** : `Opportunité`

**Titre** : `Un marché de $16 Mds\ndominé par des acteurs trop chers`

**Subtitle** : `Le MES est le prochain domaine B2B à être disrupté par l'open source.`

**3 stat-cards** :
| # | Num | Label |
|---|-----|-------|
| 1 | `16 Mds$` | Marché mondial du MES en 2025 |
| 2 | `12%/an` | Croissance annuelle |
| 3 | `160k+` | PME industrielles cibles BE · FR · pays germanophones |

**État anim actuel** : counters + stagger, plat après.

**🎯 Animation à enrichir** : sensation de **grandeur du marché**.
- Counters spectaculaires (vitesse variable, le chiffre se "verrouille" en tapant)
- Map subtile en background, ou geographic accent (BE/FR/DE/AT/CH highlighted briefly)
- Le `$16 Mds` du titre pourrait avoir un treatment spécial (gradient sweep, scale beat)
- Animer la croissance 12%/an avec une mini courbe SVG qui se trace

---

### S8 — Business Model

**Tag** : `Business Model`

**Titre** : `Gratuit pour entrer.\nPayant pour scaler.`

**Subtitle** : `Le même modèle qu'**Odoo**, appliqué au MES.`

**3 cards** (la Premium est `featured`) :
| Plan | Prix | Bullets |
|------|------|---------|
| **Open Source** | Gratuit · Toujours | Auto-hébergeable / Code source complet |
| **Premium** ⭐ | 59 €/mois/équipement | Modules avancés : IA, intégration ERP, production par lots / Connecteurs industriels |
| **Enterprise** | 95 €/mois/équipement | Tout Premium inclus / Support + installation clé en main |

**État anim actuel** : cards stagger, listes `<li>` jamais animées.

**🎯 Animation à enrichir** :
- Cards qui s'élèvent depuis le bas avec depth différentielle
- La card Premium (`featured`) doit **clairement dominer** : entrée plus tardive, plus haut, glow plus intense, peut-être un "POPULAIRE" ribbon qui se draw
- Bullets `<li>` qui apparaissent en stagger après l'entrée de la card parente
- Prix qui "verrouille" avec un counter (0 → 59 / 0 → 95)

---

### S9 — Traction ⭐ PRIORITÉ #3

**Tag** : `Traction & Roadmap`

**Titre** : `De zéro à un produit\nen 1 an`

**Subtitle** : `8 mois de développement. **5 early adopters signés**. Premier déploiement en juin.`

**Layout deux colonnes** :

**Gauche — Timeline verticale** (6 étapes) :
| Date | Statut | Événement |
|------|--------|-----------|
| Sept 2025 | ✓ done | Premier MVP opérationnel |
| Oct – Déc 2025 | ✓ done | Productivité (OEE) complète, cockpit, connexion aux machines |
| Jan – Avr 2026 | ✓ done | 39 widgets, historique des arrêts, chatbot IA, interface en 10 langues |
| **Mai 2026 · maintenant** | ✓ done **NOW** | **5 early adopters ont signé** |
| Juin 2026 | → next (amber) | **Premier déploiement** — version commercialisable |
| Q3 – Q4 2026 | Q4 | Production par lots, partenaires intégrateurs, lancement en Belgique |

**Droite — Highlight stat** :
- Big stat : `5`
- Label : `Early adopters signés`
- Sub : `Premier déploiement\n**Juin 2026**`

**État anim actuel** : timeline en bloc, NOW pas mis en valeur.

**🎯 Animation à enrichir** :
- **Ligne verticale** qui se trace progressivement (DrawSVG) du haut vers le bas
- **Dots** qui s'allument **un par un** au fur et à mesure que la ligne passe, avec le checkmark qui se dessine après le dot
- **Étape NOW** (Mai 2026) : pulse + glow + scale. C'est le moment fort.
- **Étape Juin 2026** (futur) : entre en dernier, en amber, avec un effet "à venir" (peut-être en pointillé puis se solidifie)
- **Big stat "5"** : counter, mais avec un treatment fort (échelle gauge-like, glow swell)
- Possibilité de sync timeline + big-stat pour qu'au moment où le dot NOW s'allume, le "5" apparaît à droite

---

### S10 — L'Équipe

**Tag** : `L'équipe`

**Titre** : `Expertise industrielle\n+ énergie académique`

**Subtitle** : `4 cofondateurs · **Incubés par AgiNtech** (20+ ans d'industrie).`

**4 team cards** (photos) :
| Photo | Nom | Rôle |
|-------|-----|------|
| `img/member_adam.jpg` | Adam Bernard | Frontend / UX |
| `img/member_nathan.png` | Nathan Moreau | Backend / Architecture |
| `img/member_juliette.jpg` | Juliette Marchand | Commercial / Stratégie |
| `img/membre_louis.jpeg` | Louis Verbeeren | Finance / Juridique |

**2 mentor cards** (icônes) :
| Nom | Rôle |
|-----|------|
| Christophe Camerlynck | CEO AgiNtech · 20+ ans industrie |
| Peter Mees | Expert MES · AgiNtech |

**État anim actuel** : photos en grayscale, stagger basique.

**🎯 Animation à enrichir** :
- Photos en grayscale qui passent en couleur **une par une** au stagger (= "ils prennent vie")
- Léger lift / depth pour les founders vs mentors (hiérarchie visuelle)
- Peut-être un effet "polaroid develops" (appear + slight tilt + settle)
- Ligne de connexion entre founders et mentors (visualiser l'incubation AgiNtech)

---

### S12 — L'Ask

**Tag** : `Ce qu'on cherche`

**Titre** : `On ne cherche pas\ndes applaudissements`

**Subtitle** : `Mais des connexions concrètes pour passer à l'échelle.`

**3 ask-cards** :
| # | Icône | Titre | Description |
|---|-------|-------|-------------|
| 1 | building | **Clients pilotes** | PME industrielles belges pour valider en conditions réelles. Déploiement gratuit. |
| 2 | users | **Partenaires intégrateurs** | Sociétés d'automatisation industrielle pour distribuer OpSee. |
| 3 | globe | **Visibilité & réseau** | Connexions dans l'écosystème industriel belge et européen. |

**Punchline** : `**Vous connaissez une PME industrielle ?** Présentez-nous. On fait le reste.`

**État anim actuel** : stagger trivial, punchline isolée.

**🎯 Animation à enrichir** :
- Cards qui s'élèvent avec depth, icônes qui se draw individuellement (DrawSVG)
- Hover micro-interactions (déjà en CSS ? renforcer)
- La **punchline finale** mérite un beat dédié : entre après les 3 cards, peut-être avec un highlight progressif sur "Vous connaissez une PME industrielle ?"
- Petite icône call-to-action animée à côté de la punchline

---

### S13 — Closing ⭐ PRIORITÉ #2

**Contenu** :
- Logo XL : `img/logo_texte.svg`
- Tagline rolling 3 colonnes :
  - Col 1 : `Open / Smart / Scalable` (boucle)
  - Col 2 : `Smart / Scalable / Open` (boucle, offset 1)
  - Col 3 : `Scalable / Open / Smart` (boucle, offset 2)
  - Séparées par ` · `
- Closing text :
  > Le seul MES **open source, modulaire, avec IA intégrée**.
  > **Plus jamais une PME laissée à l'aveugle.**
- 3 chips contact :
  - 🌐 www.opsee.io
  - ✉️ adam@opsee.io (cf-protected)
  - 📞 +32 71 256 280
- Tag final : `Turn complexity into clarity` (scramble text)

**État anim actuel** : logo scale, rolling auto, chips fade.

**🎯 Animation à enrichir — TRAVAIL PRINCIPAL** :
C'est la **dernière image qui reste en tête**. Elle doit clore le pitch sur un sommet.

Idées combinables :
- **Logo** : entrée majestueuse — draw SVG des lettres, particle assembly, glow swell, ou décomposition/recomposition
- **Tagline rolling** : repenser. Au lieu d'un rolling vertical mécanique, peut-être les 3 mots arrivent **séparément** depuis 3 directions, se positionnent, puis le rolling démarre. Ou : rolling pendant 3 cycles, puis **freeze sur "Open · Smart · Scalable"** définitivement.
- **Closing text** : "Plus jamais une PME laissée à l'aveugle" — phrase de fermeture émotionnelle, mérite un beat fort (peut-être l'avant-dernier, juste avant le tag final).
- **Tag final "Turn complexity into clarity"** : scramble actuel OK, mais peut être renforcé (apparition lente, puis ScrambleText, puis lock).
- **Background** : possibilité d'un événement final type "lights converge" (tous les particles convergent vers le logo, puis dispersent).

---

### Slides Backup (Q&A jury — accessibles via ESC)

Ces slides ne sont jouées que si le jury pose des questions. Animation **moins critique**, mais doivent rester cohérentes.

- **`s-backup-intro`** : Q&A frame
- **`s11`** : Avantage concurrentiel — 6 différenciateurs (Open Source, Modulaire, Offline-first, Conforme ISA-95/88, IA intégrée, Made in Belgium)
- **`s-data-problem`** : sources des chiffres du problème (67%, 99.8%, 500k€, 18 mois)
- **`s-data-market`** : sources des chiffres du marché ($16 Mds, 12%/an, 160k+)
- **`s-sources`** : bibliographie complète (9 références académiques + industrielles)

**🎯 Animation à enrichir** : si tu as le temps, enrichis S11 (6 cards). Les sources peuvent rester sobres.

---

## 6. PRIORISATION DES "MOMENTS WOW"

Voici l'ordre dans lequel tu dois investir ton effort. **Si tu n'as pas le temps de tout faire, fais ça dans cet ordre.**

| Rang | Slide | Pourquoi c'est prioritaire |
|------|-------|----------------------------|
| **1** | **S4 — Produit** | C'est ici qu'on prouve que ça existe. Slide la plus importante du deck. Doit être cinématique. |
| **2** | **S13 — Closing** | Dernière image en tête. Doit clore sur un sommet mémorable. |
| **3** | **S9 — Traction** | Raconte le voyage. Timeline animée + NOW highlight + big-stat 5 = narratif fort. |
| **4** | **S2 — Problème** | Vient juste après S1B. Doit faire ressentir la douleur. |
| **5** | **S5 — IA** | Faire vivre le dialogue user→IA. Différenciateur produit. |
| 6 | S3 — Solution | Transition contrastée vers S2. |
| 7 | S7 — Marché | Sensation de grandeur. |
| 8 | S8 — Business model | Hiérarchie Premium. |
| 9 | S10 — Équipe | Humanité. |
| 10 | S12 — Ask | Punchline finale. |
| 11 | S11 backup | Si reste du temps. |

---

## 7. STANDARDS DE QUALITÉ

### Référence absolue

**S1 (gauge 67%) et S1B (MES explainer)** sont la baseline. Ouvre leur code, observe :
- L'**orchestration multi-couches** (rings → ticks → number → fill+counter sync → impact pulse)
- Les **delays explicites** qui contrôlent le timing global plutôt que des `.then()`
- Les **moments d'impact** (pulse à la fin du fill, glow swell)
- Le **soin du détail** (filtres drop-shadow, gradients, easing custom)

**Si une nouvelle anim n'a pas la même densité chorégraphique que S1, elle n'est pas finie.**

### Règles de craft

- **60 fps non négociable.** Préfère `transform` et `opacity` à `width/height/top/left`. Évite `box-shadow` animé sur grandes surfaces (utilise `filter: drop-shadow` ou un pseudo-élément). Limite les `blur` excessifs.
- **Easing : pas de `linear`, pas de `ease`** (vague). Utilise `power2.out`, `power3.out`, `power4.inOut`, `back.out(1.5)`, `expo.out`, ou des `CustomEase` créés explicitement.
- **Durées contrôlées.** Pitch de 5min, chaque slide a 20-30s à l'écran. Anims d'entrée totales ≤ **2-3s** (S1 fait ~4s mais c'est l'ouverture). Pas d'anim qui démarre à `delay: 5`.
- **Stagger > tout-en-bloc.** Si plusieurs éléments similaires entrent ensemble, ils doivent staggerer (0.05s à 0.15s selon la densité).
- **Hiérarchie visuelle dans le timing.** Le titre rentre avant le subtitle, qui rentre avant le corps. Pas l'inverse.
- **Pas d'animation gratuite.** Chaque mouvement doit avoir un sens narratif (insister, révéler, enchaîner). Si une anim n'apporte rien, vire-la.
- **Cohérence de la palette de mouvement.** Si tu fais un fade-up de 30px sur une slide, garde 30px sur les autres slides de même nature. Pas 30 ici, 50 ailleurs, 15 plus loin.

### Checklist avant de "valider" une slide

- [ ] L'animation rejoue proprement quand on quitte/revient (`freezeContents()` à jour)
- [ ] 60 fps dans Chrome DevTools (Performance tab, record une lecture)
- [ ] Pas de flash visuel à l'entrée
- [ ] Tous les éléments sont visibles à la fin de l'anim (rien n'est resté à `opacity: 0`)
- [ ] Le timing total ≤ 3s (sauf S1 et exceptions justifiées)
- [ ] Le contenu textuel est inchangé, **bit-perfect**
- [ ] La hiérarchie titre > subtitle > corps est respectée dans l'ordre d'apparition
- [ ] Cohérence visuelle avec S1/S1B (même tonalité de mouvement)

---

## 8. NAVIGATION & TRANSITIONS

### Navigation

- **Flèche droite / espace** : slide suivante
- **Flèche gauche** : slide précédente
- **ESC** : ouvre les slides backup (Q&A)
- **Flèches dans backup** : naviguer dans backup
- **ESC dans backup** : retour à la slide principale

### Transition inter-slides actuelle

SVG shape-overlay : 2 paths qui se draw 0%→100% avec stagger, puis reverse.

**🎯 Marge d'amélioration** : la transition actuelle est fonctionnelle mais peu mémorable. Tu peux la repenser, à condition que :
- Elle reste **rapide** (≤ 0.6s aller, ≤ 0.5s retour)
- Elle ne **masque pas** l'animation d'entrée de la slide suivante (timing critique)
- Elle reste cohérente sur tout le deck

Idées : morphing shape, color sweep, particle wipe, depth zoom, etc.

---

## 9. WORKFLOW RECOMMANDÉ

1. **Lis ce fichier en entier.** Re-lis la section 1 (règles absolues).
2. **Ouvre `index.html`** et lis :
   - Le tuning panel (lignes 28-87)
   - `animateS1` (lignes 793-869) — c'est ta référence
   - `animateS1B` ou la logique mes-stack (cherche `mes-stack` dans le JS)
   - `freezeContents` (lignes 967-1050)
   - Les handlers `data-a` (lignes 1048-1180)
3. **Lance le serveur local** (probablement `python3 -m http.server` ou similaire — vérifie le README) et ouvre `index.html` dans un navigateur.
4. **Joue le deck en entier**, slide par slide, pour ressentir le rythme actuel.
5. **Attaque dans l'ordre de priorité** (section 6) :
   - Commence par S4 (produit)
   - Puis S13 (closing)
   - Puis S9 (traction)
   - etc.
6. **Pour chaque slide** :
   - Crée `animateSX(s)` en suivant le pattern de `animateS1`
   - Appelle-la dans le switch d'entrée de slide
   - Ajoute le reset symétrique dans `freezeContents()`
   - Teste : entre, sors, reviens. L'anim doit rejouer proprement.
   - Vérifie 60fps dans DevTools.
7. **Avant de "finir"**, parcours toute la checklist section 7.

---

## 10. CONTRAINTES ENVIRONNEMENT

- **Branche git** : `main` (le repo est `BERNARD-Adam/opsee-pitch`)
- **Pas de framework** : c'est du HTML/CSS/JS vanilla + GSAP. Pas de bundler, pas de build step.
- **Images** : déjà présentes dans `img/`. Tu peux les utiliser, mais n'en ajoute pas (sauf SVG décoratif inline).
- **Fichier** : tout reste dans `index.html`. Pas de fichier JS/CSS externe à créer (sauf si vraiment justifié pour la lisibilité d'un module GSAP très gros — auquel cas, mets-le dans un sous-dossier et import via `<script src="...">`).

---

## 11. DEADLINE

**Pitch le mercredi 13 mai 2026.** Date du brief : 6 mai 2026. → **7 jours**.

Priorise. Si tu dois choisir entre "5 slides moyennement améliorées" et "3 slides spectaculaires + 7 slides au statu quo", **choisis l'option 2**. La force du pitch viendra des moments wow, pas de l'uniformité.

---

## 12. EN CAS DE DOUTE

- **Si tu hésites à modifier le wording d'un texte** → ne le fais pas. Les mots sont sacrés.
- **Si tu hésites à supprimer ou ajouter un mot/une phrase/un élément informatif** → ne le fais pas. Demande.
- **Si tu hésites à réorganiser le layout d'une slide** (splitter un bloc, déplacer une stat, changer la hiérarchie visuelle) → **vas-y, c'est autorisé** tant que les mêmes mots restent à l'écran à la fin.
- **Si tu hésites à ajouter une dépendance** → ne le fais pas. Cherche une solution GSAP pure.
- **Si tu hésites sur le ton** → relis S1. Si ton anim a la même densité, tu es bon. Sinon, pousse plus loin.
- **Si une slide te semble "déjà bien"** → pousse quand même. L'objectif n'est pas "OK", c'est **wow**.

---

## TL;DR (si tu ne dois retenir qu'une chose)

> **Le pitch raconte qu'OpSee = premier MES open source pour PME industrielles, débloquant un marché de $16 Mds verrouillé par Siemens/SAP.**
>
> **Les mots du deck sont figés, mot pour mot — aucun ajout, aucune suppression, aucune reformulation.** Mais tu as toute liberté pour **réorganiser visuellement** chaque slide (splitter un bloc en deux, déplacer un élément, changer la hiérarchie, recomposer le layout) tant que les mêmes mots se retrouvent à l'écran à la fin.
>
> **Ta mission** : transformer ce deck déjà solide en un keynote Apple-grade, plein d'animations chorégraphiées, avec des moments wow sur **S4 (produit)**, **S13 (closing)** et **S9 (traction)** en priorité.
>
> **Référence du niveau attendu** : la slide **S1 (gauge 67%)** déjà en place.

Bon courage. Fais en sorte que les 4 jurés se disent : *"ils ont passé combien de temps là-dessus ?"*
