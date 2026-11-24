# 42uino mini — Bootcamp Électronique : Prototypage

Assemblage à la main des deux versions de la 42uino mini (ATmega328P, 16 MHz) : la version **THT** (composants traversants) et la version **SMD** (composants montés en surface).

Le résultat est imparfait. J'ai eu beaucoup de mal pendant ce projet, mais j'ai dû corriger presque tous les types d'erreurs possibles, et c'est ce qui m'a le plus appris.

## Processus suivi

### Préparation

- Fer réglé autour de 300 à 315°C, poste ventilé.
- Panne nettoyée (laiton) puis étamée avant chaque série de soudures. Au début, je ne l'ai pas assez fait (voir Difficultés).

### Carte THT

Du centre vers les bords, du plus grand au plus petit composant.

1. Support / ATmega328P au centre, puis quartz et bouton reset.
2. Barrettes latérales 1×12 et connecteur FTDI 1×06.
3. Composants bas : résistances, condensateurs céramiques, LEDs (en respectant la polarité).

Pour chaque joint, je chauffe en même temps le plot et la patte pendant 1 à 2 s, j'apporte la soudure du côté opposé à la panne, je retire la soudure puis la panne, et je coupe la patte au ras du cône.

### Carte SMD

1. **ATmega328P (TQFP-32)** : j'étame un plot de coin, je pose la puce à la pince, je soude ce coin, puis le coin opposé. Je vérifie l'alignement des 4 côtés à la loupe avant de souder le reste des pattes, avec beaucoup de flux.
2. **Composants 0603** (R, C, LEDs) : j'étame un plot, je pose le composant à la pince, je refonds le premier plot, puis je soude le second.
3. **Quartz 3225**, bouton B3U, puis les connecteurs THT.

### Inspection et test

- Contrôle à la loupe : joints en cône, pas de ponts, orientation des LEDs, de la puce et des connecteurs.
- Flash du bootloader puis d'un programme de test (blink).

## Observations

- **La propreté de la panne fait presque tout.** Une panne oxydée ne transmet pas la chaleur : la soudure reste en boule sur la panne et ne mouille ni le plot ni la patte. Avec une panne propre et étamée, le même joint se fait en une seconde.
- **Il faut plus de flux que ce qu'on croit**, surtout en SMD. Avec assez de flux, la soudure va d'elle-même sur les plots et quitte les espaces entre les pattes.
- **Il faut moins de soudure que ce qu'on croit.** Presque tous mes défauts viennent d'un excès de soudure (ponts, trous bouchés, quartz noyé).
- **Mes joints THT** (photo de dessous) sont pour la plupart corrects, mais certains sont ternes ou trop chargés. Ce sont ceux que j'ai faits au début, avec une panne sale, ou ceux que j'ai repris plusieurs fois.
- **Sur la carte SMD**, on voit encore un leger excès de soudure autour du quartz.

## Difficultés et solutions

### Chauffe insuffisante

Au début, je n'arrivais pas à chauffer les composants : la soudure ne coulait pas et les joints étaient froids et granuleux. Je ne comprenais pas à quel point il fallait nettoyer la panne au départ.

**Solution :** nettoyer la panne au laiton, l'étamer tout de suite, et recommencer souvent. Je mets une petite goutte de soudure sur la panne pour qu'elle conduise la chaleur au joint, et je fais toucher la panne au plot et à la patte en même temps.

### Tremblements et micro-soudure SMD

Je tremble, ce qui rend très difficile le placement des 0603 et la soudure des pattes du TQFP.

**Solutions :**

- poser les poignets et les avant-bras sur la table, et tenir le fer comme un stylo, le plus court possible ;
- pré-étamer un plot pour n'avoir à tenir que le composant et le fer, sans le fil de soudure ;
- fixer d'abord un seul point, corriger l'alignement en refondant ce point, puis souder le reste ;
- ne pas chercher à faire une soudure parfaite du premier coup : souder, puis corriger les ponts au flux et à la tresse.

### Erreurs rencontrées et corrections

| Erreur | Cause | Correction |
|---|---|---|
| **Trous THT bouchés** | Soudure en trop qui a rempli un trou avant que le composant soit posé | Chauffer le trou et aspirer à la pompe à dessouder, ou utiliser la tresse. Sinon, chauffer d'un côté et pousser la patte depuis l'autre côté. |
| **Ponts entre plots / pattes** | Trop de soudure, panne trop grosse pour le pas du TQFP | Ajouter du flux, puis passer la panne propre le long des pattes vers l'extérieur. Si le pont reste, utiliser la tresse à dessouder. |
| **Barrette THT montée à l'envers** | Orientation pas comprise avant de souder toutes les broches | Dessouder les broches une par une (pompe), en chauffant peu pour ne pas faire fondre le plastique, puis remonter la barrette dans le bon sens. |
| **Quartz SMD noyé dans la soudure** | Trop de soudure sur les 4 plots, qui sont presque cachés sous le boîtier, avec un risque de court-circuit dessous | Flux, puis tresse pour retirer l'excès. |
| **Résistances THT inversées** | Deux valeurs échangées à cause d'une mauvaise lecture du code couleur | Dessouder les deux résistances, vérifier leur valeur, puis les ressouder au bon emplacement. |
| **Joints froids / ternes** | Panne sale, chauffe trop courte | Ajouter du flux et refondre le joint avec une panne propre jusqu'à obtenir un cône brillant (fait sur le SMD). |

## Bonus

- **Reprendre un joint en le dessoudant et le ressoudant** : je l'ai fait de nombreuses fois sur les deux cartes (malgré moi).
- **Soudure en traînée pour le SMD** : j'ai fait de mon mieux pour les réussir sur le MCU et les 0603.

## Bilan

Ces cartes sont loin d'être parfaites, mais ce projet m'a appris à diagnostiquer et réparer mes erreurs : savoir pourquoi un joint est raté et comment le reprendre sans abîmer la carte. Pour la prochaine fois : **panne propre en permanence**, plus de flux, moins de soudure, et vérifier l'orientation de chaque composant avant de souder sa deuxième patte.
