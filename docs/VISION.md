# 🇹🇭 Thai Training OS — Product Vision & Master Brief

> Document source (rédigé par le porteur du projet). Il sert d'entrée au PRD technique : [`PRD.md`](./PRD.md).
> Ce fichier est conservé tel quel comme référence produit ; les décisions techniques vivent dans le PRD.

---

## 1. Vision

Créer une plateforme d'apprentissage du thaï extrêmement efficace, exigeante et mesurable, conçue autour d'un principe fondamental :

> **Le système doit mesurer ce que l'utilisateur sait réellement faire en thaï, et non simplement mesurer son activité dans l'application.**

L'objectif initial est de construire un outil personnel pour apprendre le thaï jusqu'à un niveau très avancé, potentiellement C1/C2.

Si le système fonctionne réellement sur le fondateur et démontre qu'il améliore fortement ses compétences, le produit pourra ensuite devenir un SaaS destiné à d'autres apprenants.

Le produit doit être pensé dès le départ comme une infrastructure d'apprentissage à long terme, mais le MVP doit rester suffisamment simple pour être développé et testé rapidement.

## 2. Problème

Les applications classiques d'apprentissage des langues ont plusieurs défauts :

- elles récompensent principalement l'activité ;
- elles donnent souvent une impression de progression supérieure au niveau réel ;
- elles mélangent connaissance de vocabulaire et capacité à comprendre une langue ;
- elles utilisent beaucoup de contenu artificiel ;
- elles ne mesurent pas correctement la compréhension orale ;
- elles ne mesurent pas suffisamment la vitesse de compréhension ;
- elles donnent rarement un diagnostic précis des faiblesses ;
- elles ne savent pas toujours distinguer une réponse réellement correcte d'une réponse approximative ;
- elles utilisent souvent la traduction comme intermédiaire permanent ;
- elles sont rarement adaptées aux spécificités d'une langue comme le thaï.

Le produit doit résoudre cela avec une approche proche d'un système d'entraînement sportif. L'utilisateur doit savoir :

- Où suis-je réellement ?
- Qu'est-ce que je sais faire ?
- Qu'est-ce que je ne sais pas faire ?
- Pourquoi je me trompe ?
- Quelle compétence dois-je entraîner maintenant ?

## 3. Philosophie fondamentale

### 3.1 XP ≠ niveau

Le produit doit avoir au minimum deux concepts séparés :

**XP** — score ludique servant à : récompenser l'activité ; maintenir une streak ; débloquer des éléments ; créer une sensation de progression. L'XP peut être généreuse.

**Skill Rating** — mesure sérieuse des capacités. Elle doit être difficile à augmenter et basée sur les performances réelles.

Le produit ne doit jamais permettre à un utilisateur de « grinder » son niveau simplement en faisant beaucoup d'exercices faciles.

## 4. Principe d'honnêteté

C'est probablement le principe produit le plus important. Le système doit préférer « Je ne sais pas » à « Je pense que c'est probablement ça » lorsque le système n'a pas suffisamment de confiance.

Cela concerne particulièrement : reconnaissance vocale ; prononciation ; réponses libres ; traduction ; correction grammaticale ; identification de mots ambigus.

Le système doit disposer d'un concept de **confidence** :

```
Pronunciation score: 84/100
Confidence: HIGH
```

ou :

```
Pronunciation score: —
Confidence: LOW
The recording was not clear enough to reliably evaluate your tone.
```

Une incertitude ne doit pas injustement faire perdre des points à l'utilisateur.

## 5. Exemple fondamental : ไม่

Le système doit être capable de comprendre l'intention sans pour autant accepter aveuglément une réponse incorrecte. Exemple : l'utilisateur tape `mai`, la cible est `ไม่`. Le système peut identifier que l'utilisateur vise probablement le bon mot, mais la conséquence dépend du type d'exercice.

- **Exercice de vocabulaire** — « Quel mot signifie "non" ? » → `mai` → **Correct**.
- **Exercice de transcription thaïe** — « Écris le mot en thaï. » → `mai` → **Incorrect**, mais afficher :

```
You probably meant: ไม่
Meaning: no / not
Pronunciation: mâi
Tone: falling
Your answer was semantically correct, but this exercise requires Thai script.
```

- **Exercice de prononciation** — l'orthographe saisie ne doit avoir aucun impact. Le système analyse uniquement l'audio.

## 6. Romanisation

L'objectif final est de ne plus dépendre de la romanisation. La romanisation est une béquille pédagogique temporaire.

Au début : `ไม่ / mâi / not / no` — puis progressivement : `ไม่ / not / no` — puis finalement : `ไม่`.

Le système doit supprimer progressivement la romanisation **en fonction de la compétence Reading**, et non simplement après X jours. Objectif final : l'utilisateur lit directement le thaï sans passer mentalement par l'alphabet latin.

## 7. Objectif spécifique de lecture

L'utilisateur doit pouvoir : lire rapidement le thaï ; reconnaître les caractères ; comprendre les mots ; comprendre les phrases ; comprendre des textes ; taper rapidement en thaï sur téléphone ; regarder du contenu thaï sous-titré ; progressivement lire des contenus authentiques.

La capacité à taper en thaï au clavier est une compétence explicite du produit.

## 8. Architecture des compétences

Le système doit séparer les compétences. Minimum : Vocabulary, Reading, Listening, Grammar, Writing, Speaking, Pronunciation.

Potentiellement plus tard : Reading Speed, Listening Speed, Thai Script, Spelling, Naturalness, Conversation, Pragmatics, Register.

Chaque compétence possède son propre Rating. Exemple :

```
Reading       510
Listening     390
Grammar       470
Writing       350
Speaking      410
Vocabulary    580
Pronunciation 380
```

## 9. Niveau global

Le niveau global ne doit pas être une moyenne naïve. L'utilisateur ne devrait pas pouvoir être considéré globalement A2 simplement parce qu'il possède beaucoup de vocabulaire. Le système doit intégrer une notion de **bottleneck**. Le niveau global doit refléter ce que l'utilisateur peut réellement faire dans plusieurs dimensions.

## 10. CEFR

Référence : Pre-A1, A1.1, A1.2, A2.1, A2.2, B1.1, B1.2, B2.1, B2.2, C1.1, C1.2, C2.

Le produit ne prétend pas délivrer une certification CEFR officielle. Il fournit une **CEFR-equivalent estimate** basée sur les performances observées, idéalement avec des critères différents selon chaque compétence.

## 11. Skill Rating

Le Rating doit être conçu comme un système statistique sérieux. Une réponse facile ne doit presque pas augmenter le Rating ; une réussite sur un exercice difficile doit avoir davantage d'impact.

Facteurs : difficulté estimée ; historique de l'utilisateur ; taux de réussite ; nombre d'essais ; temps de réponse ; utilisation d'indices ; type d'exercice ; compétence testée ; confiance du système ; éventuellement stabilité de la performance.

Le système doit éviter les fluctuations absurdes. Un utilisateur ne doit pas passer de A1 à A2 après cinq bonnes réponses.

## 12. Evidence-based proficiency

Chaque niveau doit être basé sur suffisamment de preuves. Exemple — pour débloquer A2 Listening, démontrer sa capacité à : comprendre des phrases courantes ; comprendre des questions ; comprendre des conversations courtes ; identifier des informations précises ; comprendre plusieurs voix ; comprendre des formulations légèrement différentes ; réussir plusieurs sessions séparées dans le temps.

Le système doit éviter qu'un seul type d'exercice puisse « faker » une compétence.

## 13. Placement Test

Lors de la première utilisation, tester séparément : vocabulaire ; lecture ; compréhension orale ; grammaire ; écriture ; éventuellement prononciation. Produire un profil initial (ex. Vocabulary A1.2, Reading Pre-A1, Listening A1.0, Grammar A1.1, Writing Pre-A1) puis générer immédiatement un plan d'entraînement.

## 14. Adaptive Learning

Le système doit constamment chercher : *quel est l'exercice ayant le meilleur rapport entre difficulté et bénéfice pour cet utilisateur maintenant ?* Si Reading = A2 et Listening = A1, augmenter automatiquement la proportion de Listening (ex. Listening 45 %, Reading 20 %, Grammar 15 %, Writing 10 %, Vocabulary 10 %). Le système doit pouvoir expliquer pourquoi.

## 15. Exercices

- **Vocabulary** : recognition ; recall ; meaning ; Thai → French ; French → Thai ; context ; sentence completion ; audio recognition.
- **Reading** : word recognition ; sentence comprehension ; word ordering ; short texts ; dialogues ; stories ; authentic content.
- **Listening** : audio → meaning ; audio → word ; audio → sentence ; dictation ; comprehension ; information extraction ; natural speech.
- **Grammar** : multiple choice ; fill-in-the-blank ; sentence transformation ; error correction ; word ordering ; production.
- **Writing** : character recognition ; Thai keyboard ; spelling ; transcription ; translation ; free response ; sentence production.
- **Speaking** : repetition ; reading aloud ; answering questions ; simulated situations ; free speech.

## 16. Un même contenu doit servir plusieurs compétences

Exemple `อันนี้เท่าไหร่ครับ` : Listening (comprendre la phrase), Reading (la lire), Grammar (structure interrogative), Vocabulary (reconnaître `เท่าไหร่`), Writing (transcrire), Speaking (prononcer). Un même élément linguistique est renforcé par plusieurs angles.

## 17. Listening Gym

Le Listening doit être une partie majeure du produit.

- **Débutant** : voix claire ; vitesse contrôlée ; phrases courtes ; vocabulaire connu.
- **Intermédiaire** : vitesse normale ; différentes voix ; phrases plus longues ; variations de formulation.
- **Avancé** : locuteurs naturels ; accents ; slang ; hésitations ; réduction phonétique ; bruit ambiant ; conversations ; YouTube ; podcasts ; interviews ; presse.

Objectif : comprendre le thaï réel, pas uniquement le thaï pédagogique.

## 18. Diversité des locuteurs

Introduire progressivement : hommes ; femmes ; jeunes ; personnes âgées ; différentes régions ; différentes voix ; différents niveaux de formalité ; différents accents lorsque pertinent. Éviter « je comprends cette voix » ; viser « je comprends le thaï ».

## 19. Authentic Content

À mesure que le niveau augmente, intégrer : YouTube ; interviews ; journaux ; articles ; conversations ; posts publics ; vidéos ; dialogues naturels ; contenu du quotidien. Le système analyse le contenu et estime :

```
Estimated level: B1.2
Known vocabulary: 91%
Unknown vocabulary: 9%
Grammar difficulty: B1
Listening difficulty: B2
Recommended: YES
```

## 20. Authenticity progression

A1 : thaï très contrôlé. A2 : conversations simples. B1 : contenu semi-authentique. B2 : contenu authentique majoritaire. C1 : contenu natif complexe. C2 : contenu natif sans simplification.

## 21. Reading Gym

La lecture commence très petit : `กิน` → `กินข้าว` → `ฉันกินข้าว` → `วันนี้ฉันกินข้าวกับเพื่อน` → paragraphes → textes → contenus authentiques.

Mesurer : exactitude ; vitesse ; vocabulaire reconnu ; compréhension ; capacité à inférer le sens ; fatigue éventuelle.

## 22. Reading Speed

Compétence distincte (ex. Accuracy 94 %, Reading speed 145 characters/min, Comprehension 91 %). La vitesse devient progressivement un facteur important à partir d'un certain niveau.

## 23. Listening Speed

Même principe. Distinguer Listening – Slow / Normal / Fast-Natural. La progression doit aller vers le naturel.

## 24. Writing

Objectif principal : la capacité à taper en thaï (pas nécessairement l'écriture manuscrite dans le MVP).

Progression : Latin → Thai script ; word completion ; sentence ordering ; transcription ; dictation ; translation ; free writing.

Évaluer : orthographe ; choix des mots ; grammaire ; naturalité ; compréhension de la consigne.

## 25. Intelligent Answer Evaluation

Les réponses libres ne doivent pas être évaluées uniquement par comparaison exacte (ex. « Je vais au restaurant demain » a plusieurs formes correctes). Distinguer :

- **Correct** — sens + grammaire + formulation acceptable ;
- **Mostly correct** — sens correct mais erreur mineure ;
- **Understandable but unnatural** — compréhensible par un Thaïlandais mais formulation peu naturelle ;
- **Wrong** — erreur qui change le sens ;
- **Unknown** — le système n'est pas suffisamment certain.

## 26. Erreurs diagnostiquées

Ne pas simplement afficher « ❌ Wrong », mais :

```
Your answer: ...
Better: ...
Issue: Classifier
You used X. For this context, Thai normally uses Y.
Severity: Minor
```

Les erreurs doivent alimenter le système adaptatif.

## 27. Pronunciation / Speech Recognition

Deux niveaux : **speech recognition** (audio → transcription) et **pronunciation assessment** (comparer la production à une cible). Analyser potentiellement : consonnes ; voyelles ; tons ; durée ; syllabes ; rythme ; prononciation globale.

## 28. Règle absolue pour le scoring vocal

Ne jamais prétendre mesurer précisément quelque chose lorsque le modèle n'en est pas capable.

```
Tone: 72
Confidence: HIGH
```

versus :

```
Tone: Unable to assess reliably.
Reason: Audio quality / insufficient signal.
```

Dans le second cas : aucune pénalité injustifiée.

## 29. Tonal system

Les tons doivent être explicitement enseignés. Pour `ไม่ / mâi`, expliquer : consonne initiale ; voyelle ; finale ; marque éventuelle ; classe de consonne ; règle de ton ; ton produit. Objectif : comprendre progressivement *pourquoi* le mot se prononce ainsi.

## 30. Pronunciation feedback

```
ไม่
Overall: 84/100
Initial consonant    96
Vowel                92
Tone                 68 ⚠️
Duration             88
Confidence: HIGH
Main issue: Your vowel is close, but your tone is flatter than the target.
```

Rester pédagogique et ne pas inventer de précision impossible.

## 31. Grammar System

Enseigner la grammaire dans des contextes réels : situation → exemples → détection → explication → pratique (plutôt que « chapitre 17 »). Maintenir néanmoins une carte structurée des concepts : Questions, Negation, Classifiers, Particles, Aspect, Tense/time expressions, Comparisons, Conditionals, Relative clauses, Complex sentences, Register.

## 32. Grammar Mastery

Un concept n'est pas « acquis » après une seule réussite. Il doit être testé : dans plusieurs phrases ; avec différents vocabulaires ; en compréhension ; en production ; après un délai ; dans différents contextes.

## 33. Spaced Repetition

Conserver une logique de répétition espacée, sans séparer artificiellement le vocabulaire de la langue. Un mot peut être révisé seul, dans une phrase, à l'écoute, dans un texte, dans une réponse libre. Objectif : *retrieval in context*, pas seulement mémorisation de flashcards.

## 34. Boss Tests

Régulièrement, un test sans savoir quel type d'exercice arrive (ex. BOSS TEST — Restaurant : Listening, Reading, Grammar, Writing, Speaking). Le résultat recalibre le Rating. Les Boss Tests ont un poids important dans l'évaluation du niveau.

## 35. Anti-gaming

Empêcher : répétition excessive du même exercice ; mémorisation des réponses ; spam d'essais ; exploitation des indices ; apprentissage uniquement du format des questions. Le Rating doit utiliser des preuves diversifiées.

## 36. Progress Dashboard

```
🇹🇭 THAI
Overall        A1.2
Vocabulary     A2.0
Reading        A1.2
Listening      A1.1
Grammar        A1.2
Writing        A1.0
Speaking       A1.1
Pronunciation  A1.0

🔥 14 day streak
🎯 Main weakness: Listening
📈 Biggest improvement: Reading +42
🧠 Current focus: Natural question forms
⏱️ Weekly practice: 4h 32m
```

## 37. Diagnostic Dashboard

Le produit doit être capable de dire : « Tu connais ce mot à l'écrit mais tu ne le reconnais pas à l'oral », « Tu comprends la phrase mais tu produis incorrectement la structure », « Tu comprends le thaï lent mais pas encore à vitesse naturelle ». Ces diagnostics sont plus importants que le simple score.

## 38. Skill Bottlenecks

Identifier les obstacles principaux (ex. Listening A1.1 ← bottleneck) : « Listening is currently limiting your overall progression. » Adapter automatiquement l'entraînement.

## 39. Gamification

Doit servir l'apprentissage, pas le remplacer : XP ; streak ; daily missions ; achievements ; Boss ; skill tree ; rank ; challenges ; milestones. **XP doit être amusant. Rating doit être honnête.**

## 40. Rank

Pre-A1, A1, A2, B1, B2, C1, C2 avec subdivisions internes (A1.1, A1.2). Le Rating numérique permet davantage de granularité (ex. Thai Rating 427 — CEFR estimate A1.2).

## 41. Long-term goal

Accompagner un utilisateur pendant plusieurs années : Absolute beginner → A1 → A2 → B1 → B2 → C1 → C2. Contenu, exercices, voix, complexité et sources évoluent avec l'utilisateur.

## 42. Native immersion

Retirer progressivement les éléments pédagogiques artificiels :

- **A1** : thaï, traduction française, romanisation, audio lent ;
- **A2** : thaï, français occasionnel, audio normal ;
- **B1** : thaï, explications de plus en plus en thaï, audio naturel ;
- **B2+** : thaï, explications en thaï, contenu authentique ;
- **C1/C2** : thaï uniquement.

Seuil déterminé à partir des performances, pas du nombre de leçons.

## 43. Thai-only mode

Fonctionnalité dédiée pour passer progressivement à « Thai only » : consignes, définitions, feedback et contenu entièrement en thaï. Étape importante de progression.

## 44. Real-world readiness

Mesurer progressivement : « Est-ce que je pourrais réellement vivre en Thaïlande et comprendre les gens ? » — restaurant ; transport ; shopping ; travail ; logement ; administration ; small talk ; famille ; téléphone ; humour ; slang ; situations inattendues.

## 45. Content difficulty engine

Chaque contenu possède des métadonnées : Content ID, Estimated CEFR, Vocabulary difficulty, Grammar difficulty, Listening difficulty, Reading difficulty, Speech speed, Number of unknown words, Authenticity, Register, Accent.

## 46. Content recommendation

Le système doit pouvoir dire « Recommended for you » avec une justification, ex. :

```
🎧 YouTube clip
Difficulty: B1.1
Your Listening: A2.1
Known vocabulary: 89%
Why recommended: You already know most of the vocabulary, but the speaker's
natural speed will challenge your listening comprehension.
```

## 47. Mobile-first / PWA

Utilisation principalement sur téléphone. Objectif initial : website installable sur l'écran d'accueil (PWA, mobile-first). Excellente expérience sur iPhone, Android, tactile, clavier thaï, microphone, écouteurs. Une application native n'est pas nécessaire pour le MVP.

## 48. SaaS vision

Commencer comme outil personnel, mais laisser la possibilité de devenir un SaaS : comptes ; profils ; progression ; contenu ; personnalisation ; abonnements ; statistiques ; éventuellement communauté et classement. Le MVP ne doit pas être surchargé par les besoins SaaS.

## 49. Fondateur comme premier utilisateur

Premier objectif de validation : *est-ce que ce système fonctionne réellement sur moi ?* Observer : Starting level → Training → Skill ratings → Real-world tests → Progress.

La réussite n'est pas « j'ai développé une belle application » mais « après plusieurs mois, je comprends et produis réellement beaucoup mieux le thaï ».

## 50. Success Metrics

Produit : rétention ; sessions ; exercices réalisés. Mais surtout **learning outcomes** : amélioration Listening, Reading, Writing, Speaking ; compréhension à vitesse naturelle ; capacité à comprendre du contenu authentique ; progression CEFR-equivalent. Mesurer les résultats réels, pas uniquement l'engagement.

## 51. Différence fondamentale avec Duolingo

Le produit n'est pas « Duolingo mais en thaï ». C'est **un système d'entraînement adaptatif qui cherche à mesurer et améliorer les capacités linguistiques réelles d'un apprenant.**

| Approche classique | Thai Training OS |
|---|---|
| XP comme progression | XP + Skill Rating |
| Parcours linéaire | Adaptive learning |
| Exercices génériques | Exercices diagnostiques |
| Traduction fréquente | Immersion progressive |
| Audio pédagogique | Audio → thaï naturel |
| Une seule voix / style | Diversité de locuteurs |
| Correction binaire | Diagnostic détaillé |
| Prononciation approximative | Pronunciation + confidence |
| Niveau estimé par progression | Niveau basé sur preuves |
| Contenu artificiel | Contenu authentique progressif |
| Vocabulaire isolé | Vocabulaire en contexte |
| Réussite ponctuelle | Mastery démontrée |

## 52. Principes UX

Ludique (envie de revenir) ; exigeante (niveaux supérieurs réellement difficiles) ; claire (comprendre pourquoi on perd des points) ; motivante (une mauvaise réponse devient une information utile) ; honnête (ne jamais gonfler artificiellement le niveau) ; non infantilisante.

## 53. Principes de correction

Chaque correction répond idéalement à : Qu'ai-je répondu ? Qu'attendait le système ? Mon erreur est-elle grave ? Pourquoi ? Comment le dire correctement ? Dois-je revoir quelque chose ? Cette erreur a-t-elle affecté mon Rating ?

## 54. Error Memory

Mémoriser les erreurs importantes. Exemple : l'utilisateur confond régulièrement `ไม่` / `ไหม` / `ใหม่` (confidence: high) → recommandation : créer des exercices de contraste ciblés, générés automatiquement.

## 55. Intelligent contrast exercises

Pour des éléments souvent confondus, une série dédiée : Listening discrimination (écouter les trois) ; Reading discrimination (identifier les mots) ; Meaning (associer au sens) ; Production (prononcer le mot demandé) ; Context (choisir la bonne forme dans une phrase).

## 56. Personal difficulty model

La difficulté n'est pas seulement une propriété du contenu : un même exercice peut être facile pour A et difficile pour B. Le système doit apprendre le niveau réel de cet utilisateur pour ce type précis de tâche.

## 57. Long-term intelligence

À terme, produire une analyse du type :

> Arthur has strong vocabulary recognition but weak auditory retrieval. He recognizes approximately 90% of known words in written form but only 65% when spoken at natural speed. His main current bottleneck is phonological processing rather than vocabulary knowledge.
> Recommended training: short natural dialogues, dictation, minimal pairs, repeated listening, reduced use of subtitles.

Ce type de diagnostic doit être une des grandes valeurs du produit.

## 58. Future AI capabilities

L'IA pourrait servir à : générer et adapter des exercices ; corriger les réponses ; analyser les erreurs ; générer des explications et des dialogues ; analyser du contenu authentique ; estimer la difficulté ; analyser la prononciation ; créer des tests personnalisés.

Mais **l'IA ne doit pas être seule responsable de la vérité du système de scoring.** Les modèles génératifs peuvent aider à produire et interpréter, mais le système de mesure doit être déterministe/statistique/calibré autant que possible.

## 59. Calibration

Calibrer avec : exercices de difficulté connue ; performances historiques ; tests répétés ; benchmarks ; utilisateurs réels ; éventuellement évaluations humaines. Le système doit pouvoir dire « cette estimation est très fiable » ou « nous avons encore trop peu de données ».

## 60. Ce que le PRD technique devra résoudre

- **Architecture** : frontend ; backend ; database ; authentication ; PWA ; stockage audio ; CDN ; infrastructure.
- **AI** : LLM ; speech-to-text ; pronunciation assessment ; TTS ; modèles spécialisés ; orchestration ; coûts ; latence.
- **Scoring** : Skill Rating ; calibration ; difficulté ; confidence ; CEFR mapping ; decay ; uncertainty ; anti-gaming.
- **Data model** : User, Skill, Exercise, Question, Answer, Attempt, Content, VocabularyItem, GrammarConcept, PronunciationTarget, Rating, CEFRLevel, Error, Review.
- **Content system** : création ; tagging ; estimation de difficulté ; adaptation ; intégration de contenu authentique.
- **Speech** : transcription ; phoneme alignment ; tone detection ; pronunciation scoring ; confidence estimation.
- **Adaptive engine** : algorithme choisissant le prochain meilleur exercice pour cet utilisateur.

## 61. Contraintes importantes

Le système ne doit pas : gonfler artificiellement les niveaux ; donner des scores de prononciation sans confiance suffisante ; dépendre exclusivement d'un LLM pour évaluer les performances ; maintenir la romanisation trop longtemps ; entraîner uniquement la reconnaissance passive ; confondre mémorisation et maîtrise ; considérer une compétence acquise après une seule réussite ; utiliser uniquement des voix artificielles à haut niveau ; transformer l'expérience en simple jeu d'XP.

## 62. Philosophie finale

« J'ai un coach linguistique personnel + un laboratoire de mesure de mes compétences. » Chaque jour : What I know / What I don't know / What I am improving / What is holding me back / What I should practice next / How confident the system is about its assessment. Après plusieurs mois, le niveau affiché doit correspondre suffisamment à la réalité pour que l'utilisateur puisse avoir confiance dans le système.

## 63. North Star

> **If the app says I am B1 in Listening, can I actually function like a B1 listener in the real world?**

Si oui, le produit fonctionne. Si non, le système de scoring doit être amélioré, même si l'application est très engageante.

## 64. Première version à construire

- **Core** : compte utilisateur ; dashboard ; Skill Ratings ; XP ; progression ; exercices adaptatifs.
- **Thai** : vocabulaire ; lecture ; grammaire ; listening ; writing au clavier.
- **AI** : correction intelligente ; génération d'exercices ; speech-to-text initial ; première version de pronunciation assessment avec confidence.
- **Progression** : placement test ; CEFR-equivalent ; romanisation progressive ; Boss Tests ; diagnostic des faiblesses.

Le contenu authentique massif et les fonctionnalités SaaS avancées peuvent arriver ensuite.

## 65. Directive pour le PRD technique

Produire un PRD technique complet et critique, sans simplement reformuler les features : identifier les risques techniques et les fonctionnalités difficiles ; proposer plusieurs solutions et recommander ; expliquer les compromis ; distinguer MVP / V1 / V2 / long terme ; proposer une architecture scalable mais raisonnable ; définir les modèles de données, les APIs, les algorithmes de scoring, la stratégie d'évaluation vocale, le système adaptatif, la stratégie de contenu, les métriques de succès et les tests vérifiant que le système est réellement honnête.

Le PRD doit être suffisamment concret pour qu'une équipe puisse commencer à développer le MVP, tout en conservant la vision fondamentale :

> **Build a language-learning system that measures real ability rather than app activity.**
