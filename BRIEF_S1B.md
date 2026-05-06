# BRIEF — Animation S1B (MES Explainer)

> À lire après `CONTEXT_DESIGNER.md`. Ce brief te donne la **vision**, le **niveau attendu**, et les **garde-fous**. Le reste — comment exactement tu réalises l'animation — c'est ton terrain de création. Surprends-nous.

---

## 0. POURQUOI CETTE SLIDE COMPTE

Cette slide pédagogique est **le pivot narratif du pitch**. Si en 25 secondes le jury ne comprend pas viscéralement ce qu'est un MES, toutes les slides suivantes s'effondrent : pas de problème, pas de solution, pas de produit, pas de marché.

→ **C'est la slide qui doit faire dire au jury : "Ah OK, je vois exactement de quoi vous parlez."**

Le wording est déjà pédagogiquement parfait. **Ton job : rendre la compréhension instantanée et physique** par le mouvement, pas par le texte.

---

## 1. WORDING À PRÉSERVER (mot pour mot)

```
Tag         : 30 secondes pour comprendre
Titre       : C'est quoi un MES ?
Subtitle    : La tour de contrôle de l'usine.

Stack 3 tiers :
  ┌─ ERP        — "Vend & planifie"
  ├─ ★ MES      — "Pilote"
  └─ MACHINES   — "Produisent"

Punchline   : Sans MES, l'usine vole à l'aveugle.
```

**Tu peux** : recomposer le layout, splitter, déplacer, changer la hiérarchie typographique, modifier l'orientation du stack.
**Tu ne peux pas** : modifier ces mots, en ajouter, en retirer.

---

## 2. LA VISION — CE QU'ON VEUT RESSENTIR

**Trois mots qui doivent décrire ton résultat : classe, premium, épuré.**

Et un quatrième : **wow**.

Pas "wow" au sens "ça bouge dans tous les sens". Wow au sens **"j'avais jamais vu ça aussi bien fait"**. Le wow d'Apple, qui n'est jamais bruyant.

### Le DNA à reproduire

Quand tu regardes une keynote Apple sur leurs chips, leur Vision Pro, leur Dynamic Island — qu'est-ce qui te touche ?

- **La matière a du poids.** Les éléments ne flottent pas comme des stickers, ils ont une densité, une lumière intérieure, une présence.
- **Le silence est une note.** Apple chorégraphie ses pauses comme de la musique. Sans pauses, tout devient bruit.
- **Le restraint est le luxe.** Apple soustrait, ne décore pas. 2-3 choses bougent à la fois maximum, jamais plus.
- **La profondeur existe.** Avant-plan / plan moyen / arrière-plan distinguables. Du depth of field, des ombres, du parallax subtil.
- **La lumière raconte.** Glow halos, light sweeps, rim lights. La lumière est un acteur, pas un effet décoratif.
- **Le timing est musical.** Anticipation → action → recovery → silence → action. Easings suspendus, longs, jamais brusques sauf intention dramatique.

→ Si ton animation a cette **tonalité**, peu importe les détails techniques. Si elle ne l'a pas, peu importent les détails techniques.

---

## 3. LE CŒUR NARRATIF — CE QUE L'ANIMATION DOIT RACONTER

Le wording dit : ERP "Vend & planifie" / MES "Pilote" / MACHINES "Produisent". L'animation doit **rendre cela visible** sans qu'on ait besoin de lire.

### Ce qu'on veut voir, en 4 mouvements (durées, formes, détails : à toi)

**1. L'arrivée des 3 tiers** — Chacun arrive comme un objet matériel distinct. Le MES doit clairement être le **héros visuel** : il arrive en dernier, il irradie, il a son moment.

**2. La connexion** — Des canaux / artères / liens lumineux se tracent entre les tiers. Pas des lignes plates : des structures qui ont matière et lumière.

**3. Le flux qui vit** — La donnée circule. Et **le MES la transforme**.
   - Descendant : l'ERP envoie des instructions → le MES les **route / multiplie / dispatch** vers les MACHINES
   - Remontant : les MACHINES envoient des données temps réel → le MES les **agrège / synthétise** vers l'ERP
   - Cette différence de traitement (1→N à la descente, N→1 à la remontée) est ce qui **enseigne le rôle du MES** sans un mot. C'est le point pédagogique central.
   - Le système doit sembler **vivant** : le MES respire, les flux varient subtilement entre les cycles. Pas une boucle robotique perceptible.

**4. La punchline — la perte** — "Sans MES, l'usine vole à l'aveugle". On doit **physiquement ressentir** ce que devient le système quand le MES disparaît. Les flux se rompent, les machines s'éteignent, l'ERP reste seul. Ou tout autre traitement qui crée la même sensation de perte. **C'est un moment émotionnel, pas informationnel.**

→ **Avant cette punchline, laisse le silence respirer.** Une pause de quelques centaines de ms qui prépare le climax. Ce silence est essentiel.

---

## 4. ANTI-PATTERNS — LES PIÈGES À ÉVITER

Si tu reconnais une de ces tentations, **arrête et repense**. Ce sont les patterns "AI generic" qui tuent immédiatement la sensation premium.

❌ **Trois cards CSS identiques avec juste un texte différent.** ERP, MES et MACHINES doivent avoir une **matérialité visuelle distincte**. Si on enlève les labels, on doit pouvoir les distinguer rien qu'à leur look.

❌ **Petits dots ronds qui descendent en boucle linéaire.** C'est LE cliché data-flow. Tes packets de données doivent avoir forme, matière, transformation au passage du MES.

❌ **Un glow uniforme partout.** La hiérarchie de lumière est narrative : le MES irradie, les autres tiers sont plus calmes. Sinon on ne sait plus qui est le héros.

❌ **Du mouvement continu sans pause.** Sans silences, tout devient bruit. Apple alterne action/repos. Tes pauses sont aussi importantes que tes actions.

❌ **Easing `power2.out` partout.** Trop générique. Crée des `CustomEase` plus suspendus, plus signature. Exemple de courbe Apple : `"0.16, 1, 0.3, 1"` (soft suspend out).

❌ **Une boucle prévisible.** Si à 10 secondes le spectateur sait ce qui va se passer, c'est mauvais. Varie subtilement les cycles.

❌ **Particules en ligne droite robotique.** Utilise MotionPath avec des bezier subtilement courbés. Trajectoires organiques.

❌ **Trop d'éléments simultanés.** À tout moment, le spectateur doit pouvoir nommer en 1 phrase ce qui se passe. Si tu ne peux pas, c'est trop chargé.

❌ **Couleurs hors palette.** Reste strictement dans la gamme violet/blanc/sombre du deck. Le `--amber` existant peut être utilisé **uniquement** pour souligner "à l'aveugle" en finale, si tu veux.

---

## 5. NIVEAU ATTENDU — LA RÉFÉRENCE

Va voir ces moments précis sur YouTube avant de coder. Sens leur tonalité.

- **Apple M1 Ultra reveal** (mars 2022) — la fusion des 2 chips, lumière contenue dans le die
- **Apple Vision Pro intro** (juin 2023) — particules qui composent le device, depth of field
- **iPhone Dynamic Island** (sept 2022) — matière noire qui s'étire, qui respire, qui se déforme
- **Apple Pro Display XDR** (juin 2019) — les pixels qui se révèlent un par un, le noir absolu

Ce n'est **pas la complexité** qui te touche dans ces moments. C'est la **matérialité**, le **silence**, le **timing musical**, la **retenue**. Reproduis cette **sensation**, pas les détails techniques.

**Si ton animation S1B ne donne pas la même sensation premium que ces moments, elle n'est pas finie.** Compare honnêtement.

Et baseline locale : la slide **S1 (gauge 67%)** dans le même fichier (`animateS1`, ~lignes 793-869) a été soignée. Ton animateS1B doit avoir au moins la même densité d'orchestration.

---

## 6. GARDE-FOUS TECHNIQUES (les seules contraintes dures)

- **GSAP only.** Plugins déjà chargés : DrawSVGPlugin, MotionPathPlugin, ScrambleTextPlugin, CustomEase. Tu peux ajouter d'autres plugins du club GSAP si vraiment nécessaire. Aucune autre dépendance.
- **60fps non négociable.** Profile dans Chrome DevTools Performance. Préfère `transform`, `opacity`, `filter: drop-shadow`. Évite `width/height/top/left` animés et `box-shadow` animé sur grandes surfaces.
- **Maximum ~8 particules simultanées** à l'écran. Apple ne sature jamais. Si tu en as plus, tu fais probablement trop.
- **Palette stricte** : variables CSS existantes du deck (`--purple`, `--purple-light`, `--purple-dark`, `--purple-glow`, `--bg`, `--text`, `--amber`). Pas de nouvelle couleur introduite.
- **Reset/replay propre** : ajoute le state initial dans `freezeContents()` pour `s.id === 's1b'`. Test obligatoire : entrer / quitter / revenir → aucun flash, l'anim rejoue depuis zéro.
- **Timing total** : la slide est lue ~25s en pitch. Phase d'arrivée + premier cycle de flux ≤ 6s. Loop ensuite tant qu'on est sur la slide.
- **Code orchestré** dans une fonction `animateS1B(s)` claire, sur le modèle de `animateS1`. Pas du spaghetti.

---

## 7. LE TEST FINAL

Trois questions à te poser quand tu penses avoir fini. Si la réponse à une seule est "non" ou "pas sûr", **continue à itérer**.

1. **Le test du mute.** Si quelqu'un mute le pitch et regarde uniquement S1B en boucle pendant 20 secondes, peut-il expliquer **avec ses propres mots** ce qu'est un MES et pourquoi c'est important ?

2. **Le test de la comparaison.** Si tu ouvres ta S1B côte à côte avec un moment de keynote Apple (M1 Ultra ou Vision Pro), est-ce que tu n'as pas honte ? La tonalité est-elle au niveau ?

3. **Le test du restraint.** Si tu retires un élément qui t'a semblé "important d'ajouter", est-ce que ton animation est **meilleure** ? (Si oui, retire-le. L'épure est le luxe.)

---

## 8. EN CAS DE DOUTE

- Si tu hésites entre 2 options visuelles → **choisis la plus retenue.**
- Si tu hésites sur la complexité → **simplifie.**
- Si tu hésites sur la durée → **plus long et plus suspendu** plutôt que rapide saccadé.
- Si tu te dis "personne ne remarquera ce détail" → **Apple le remarque.** Fais-le.
- Si une idée te semble cliché → c'est probablement cliché. Trouve mieux.

---

## TL;DR

> Cette slide est le pivot du pitch. Le wording est intouchable, le reste est ton terrain.
>
> Construis 3 tiers avec des **matérialités distinctes** (pas 3 cards identiques). Le **MES est le héros** — il irradie, il respire, il transforme la donnée qui le traverse. Anime un flux vivant qui **enseigne sans texte** ce que fait le MES (1→N à la descente = il dispatche, N→1 à la remontée = il agrège). Termine par une rupture émotionnelle qui rend physique la phrase "vole à l'aveugle".
>
> Ton terrain de jeu : le **comment**. Surprends-nous, mais avec **classe, premium, épuré, et le wow d'Apple** — jamais bruyant, toujours retenu, toujours intentionnel. Si ton résultat ne soutient pas la comparaison avec un moment de keynote Apple, continue à itérer.
