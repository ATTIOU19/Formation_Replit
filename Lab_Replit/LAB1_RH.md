# Lab 1 — RH : système d'aide au tri des CV

> Module 3 du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** Un recruteur reçoit de nombreuses candidatures pour une offre. Lire chaque CV en détail prend un temps considérable.

**Objectif.** Construire une application qui fait un premier tri des CV, attribue à chaque candidat une note **expliquée**, et laisse la décision finale au recruteur.

**Vous allez construire**
- un formulaire de dépôt de CV et de saisie de la fiche de poste ;
- une note de 0 à 100 par critère, avec justification ;
- un tableau de classement des candidats ;
- un export des résultats.

**Vous allez apprendre**
- à rendre une décision de l'IA traçable (traçabilité d'une décision IA) ;
- à repérer les biais et les risques liés aux données personnelles (RGPD).

**Livrable final** : application déployée + cahier des charges + architecture + jeux de tests + résultats + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Définir le processus métier](#étape-0--définir-le-processus-métier) | Schéma du processus + fiche de poste |
| 1 | [Construire la grille de scoring](#étape-1--construire-la-grille-de-scoring) | Grille de scoring validée |
| 2 | [Construire l'application](#étape-2--construire-lapplication) | Application fonctionnelle |
| 3 | [Tester sur des cas piégés](#étape-3--tester-sur-des-cas-piégés) | Jeux de tests + résultats |
| 4 | [Ajouter la décision humaine](#étape-4--ajouter-la-décision-humaine) | Écran de décision humaine |
| 5 | [Discuter biais, RGPD et rôle de l'IA](#étape-5--discuter-biais-rgpd-et-rôle-de-lia) | Notes de discussion |
| 6 | [Documenter](#étape-6--documenter) | Dossier final du projet |

---

## Étape 0 : définir le processus métier

**Durée : 20 min**

Avant d'ouvrir Replit, formalisez le flux sur papier ou dans un document.

```text
CV
 ↓
Extraction
 ↓
Normalisation
 ↓
Analyse des critères
 ↓
Score
 ↓
Justification
 ↓
Validation humaine
 ↓
Classement
```

### À faire

1. Rédigez une fiche de poste fictive courte : intitulé, missions, compétences requises, expérience souhaitée, formation, langues.
   Exemple : *Assistant(e) administratif(ve)*.
2. Notez ce schéma en haut de votre futur fichier `README.md` de projet : il servira de référence pendant toute la construction.
3. Identifiez qui utilisera l'application (le recruteur) et ce qu'il attend de chaque écran.

**Résultat attendu :** un schéma du processus et une fiche de poste, prêts à être donnés à l'Agent à l'étape 2.

---

## Étape 1 : construire la grille de scoring

**Durée : 20 min**

Une note « boîte noire » n'est pas utilisable par un recruteur. Il faut une grille explicite, pondérée, que l'IA devra suivre et justifier.

### À faire

1. Choisissez 4 critères et pondérez-les pour qu'ils totalisent 100 %. Exemple :

   | Critère | Poids |
   |---|---:|
   | Compétences | 40 % |
   | Expérience | 30 % |
   | Formation | 20 % |
   | Langues | 10 % |

2. Pour chaque critère, notez 2 ou 3 indices concrets qui permettront à l'IA de noter (ex. pour « Compétences » : mots-clés attendus de la fiche de poste retrouvés dans le CV).
3. Décidez du format de la justification attendue, par exemple :

   ```text
   Compétences : 32 / 40 — 4 des 5 compétences clés sont présentes, gestion de projet absente.
   Expérience  : 21 / 30 — 3 ans sur un poste similaire, secteur différent.
   Formation   : 15 / 20 — diplôme correspondant, spécialisation manquante.
   Langues     : 6 / 10  — anglais courant, espagnol non mentionné.
   Total       : 74 / 100
   ```

**Résultat attendu :** une grille de scoring validée, avec ses poids et le format de justification.

---

## Étape 2 : construire l'application

**Durée : 60 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape avant de passer à la suivante.

### Les sept prompts

1. **Formulaire de fiche de poste et de dépôt de CV**
   > « Crée une application web avec un formulaire pour saisir une fiche de poste (intitulé, missions, compétences, expérience, formation, langues) et déposer plusieurs CV au format PDF ou Word. »

2. **Extraction du texte des CV**
   > « Ajoute l'extraction automatique du texte de chaque CV déposé, et affiche ce texte brut pour vérification. »

3. **Normalisation des informations**
   > « Structure le texte extrait en champs identifiables : nom, expériences, formations, compétences, langues. »

4. **Analyse par critère avec une note de 0 à 100**
   > « En te basant sur la fiche de poste et sur la grille suivante [colle ta grille de l'étape 1], attribue à chaque CV une note de 0 à 100, avec le détail par critère. »

5. **Justification détaillée du score**
   > « Pour chaque critère, rédige une justification courte qui explique la note donnée, dans le format suivant [colle ton format de l'étape 1]. »

6. **Tableau de bord de classement**
   > « Crée un tableau de bord qui liste tous les candidats du meilleur au moins bon score, avec le détail de chaque candidat accessible en un clic. »

7. **Export des résultats**
   > « Ajoute un bouton d'export du classement et des justifications au format CSV ou Excel. »

### Méthode

- Un prompt → un test → une correction si besoin → on passe au suivant.
- Si l'Agent produit une erreur, ne cumulez pas les instructions : demandez la correction avant de continuer (voir le module 6 du programme pour la méthode de débogage).
- Utilisez les **Secrets** de Replit pour toute clé d'API, jamais le code ni le chat.

**Résultat attendu :** une application fonctionnelle, accessible en Preview, qui va du dépôt de CV jusqu'à l'export.

---

## Étape 3 : tester sur des cas piégés

**Durée : 30 min**

Préparez ou demandez au formateur 5 CV fictifs, dont des cas volontairement difficiles :

- un CV mal mis en forme (texte mal structuré, tableaux) ;
- un très bon CV, mais hors sujet par rapport à la fiche de poste ;
- un CV incomplet (sans expérience ou sans formation) ;
- deux CV quasiment identiques, à l'exception du genre ou de l'âge du candidat.

### À faire

1. Déposez les 5 CV dans l'application.
2. Notez dans un tableau : CV testé → note obtenue → justification produite → cohérente ou non.
3. Pour le cas des CV identiques sauf genre/âge : vérifiez que les scores sont bien identiques. Si ce n'est pas le cas, c'est un signal de biais à corriger ou à documenter.
4. Demandez à l'Agent de corriger tout comportement incohérent repéré.

**Résultat attendu :** un tableau de tests avec les résultats, à conserver pour la documentation finale.

---

## Étape 4 : ajouter la décision humaine

**Durée : 15 min**

La note de l'IA n'est qu'une aide. Le recruteur doit pouvoir décider et garder la main.

### À faire

Demandez à l'Agent :
> « Ajoute pour chaque candidat une zone de décision du recruteur : Retenir / Écarter / À revoir, avec un champ de commentaire libre et la date de la décision. Cette décision doit apparaître dans le tableau de classement et primer sur la note de l'IA. »

**Résultat attendu :** un écran où le recruteur peut décider, commenter, et voir sa décision affichée à côté de la note de l'IA.

---

## Étape 5 : discuter biais, RGPD et rôle de l'IA

**Durée : 20 min**

Cette étape est une discussion, pas une construction. Prenez des notes : elles alimenteront la documentation finale.

### Points à aborder

- **Biais possibles** : âge, genre, origine, trous dans le parcours. Quelles parades avez-vous observées ou pourriez-vous ajouter ? (critères explicites, anonymisation du nom et de la photo avant analyse, relecture humaine systématique)
- **Données personnelles** : un CV est une donnée personnelle. Quelle est la base légale de son traitement ? Combien de temps le conserver ? Que dit le RGPD ou la législation locale ?
- **Rôle de l'IA** : reformulez en une phrase le principe du lab — *l'IA assiste, le recruteur décide*.

**Résultat attendu :** des notes de discussion sur les biais identifiés et les limites RGPD de l'application.

---

## Étape 6 : documenter

**Durée : 15 min**

Rassemblez tout ce qui a été produit dans un dossier de projet clair. C'est ce dossier, avec l'application déployée, qui constitue le livrable final.

### À faire

1. Déployez l'application avec le bouton **Deploy** de Replit.
2. Rédigez la fiche du projet (voir modèle ci-dessous).
3. Poussez le tout sur GitHub (voir section suivante).

### Modèle de fiche projet

```markdown
# Lab RH — Système d'aide au tri des CV

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Les grandes étapes techniques : dépôt, extraction, scoring, classement, export]

## Grille de scoring
[Votre grille de l'étape 1]

## Tests réalisés
[Votre tableau de l'étape 3]

## Décision humaine
[Comment la validation du recruteur a été intégrée]

## Biais et RGPD
[Vos notes de l'étape 5]

## Limites identifiées
[Ce que l'application ne fait pas ou ne fait pas bien]

## Lien vers l'application déployée
[URL Replit]
```

**Résultat attendu (livrable final du lab)** : application déployée + cahier des charges + architecture + tests + limites.

---

## Pousser ce lab sur GitHub

```bash
git init
git add LAB1_RH.md
git commit -m "Lab 1 RH : système d'aide au tri des CV"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

Si le dépôt existe déjà, remplacez les trois premières lignes par :

```bash
git add LAB1_RH.md
git commit -m "Ajout du lab RH"
git push
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour aller plus loin sur les Secrets, l'authentification et la traçabilité.
