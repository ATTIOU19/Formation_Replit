# Lab 5 — Project Management : suivi d'avancement et détection de dérives

> Module du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** Un chef de projet suit plusieurs tâches, avec des responsables et des dépendances entre elles. Un retard sur une tâche peut en bloquer d'autres, mais ce n'est pas toujours visible avant qu'il ne soit trop tard.

**Objectif.** Construire une application qui suit l'avancement d'un planning, détecte les tâches en retard ou à risque, estime l'impact sur la date de livraison finale, et prépare un compte rendu **prêt à valider** avant envoi au client ou à la direction.

**Vous allez construire**
- un import de planning (tâches, responsables, dates, avancement) ;
- une détection des tâches en retard ou à risque, avec justification ;
- une estimation de l'impact sur la date de livraison finale ;
- un compte rendu généré automatiquement, à valider avant diffusion.

**Vous allez apprendre**
- à raisonner sur des dépendances entre tâches plutôt que sur des lignes isolées ;
- à séparer ce que l'IA peut rédiger seule de ce qui doit rester sous contrôle humain avant d'être envoyé à un tiers.

**Livrable final** : application déployée + cahier des charges + architecture + jeux de tests + résultats + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Définir le processus métier](#étape-0--définir-le-processus-métier) | Schéma du processus + planning de référence |
| 1 | [Construire la règle de détection des dérives](#étape-1--construire-la-règle-de-détection-des-dérives) | Règle de détection validée |
| 2 | [Construire l'application](#étape-2--construire-lapplication) | Application fonctionnelle |
| 3 | [Tester sur des cas piégés](#étape-3--tester-sur-des-cas-piégés) | Jeux de tests + résultats |
| 4 | [Ajouter la validation humaine](#étape-4--ajouter-la-validation-humaine) | Écran de validation du compte rendu |
| 5 | [Discuter fiabilité et limites de l'estimation](#étape-5--discuter-fiabilité-et-limites-de-lestimation) | Notes de discussion |
| 6 | [Documenter](#étape-6--documenter) | Dossier final du projet |

---

## Étape 0 : définir le processus métier

**Durée : 20 min**

Avant d'ouvrir Replit, formalisez le flux sur papier ou dans un document.

```text
Planning (tâches, dates, avancement)
 ↓
Détection des tâches en retard ou à risque
 ↓
Analyse des dépendances
 ↓
Estimation de l'impact sur la date finale
 ↓
Rédaction du compte rendu
 ↓
Validation humaine
 ↓
Diffusion
```

### À faire

1. Construisez un planning fictif d'une dizaine de tâches avec : nom de la tâche, responsable, date de début et de fin prévues, date réelle ou avancement en %, et une ou deux dépendances (« la tâche B ne peut commencer qu'après la tâche A »).
2. Notez ce schéma en haut de votre futur fichier `README.md` de projet : il servira de référence pendant toute la construction.
3. Identifiez qui utilisera l'application (le chef de projet) et ce qu'il attend de chaque écran.

**Résultat attendu :** un schéma du processus et un planning de référence, prêts à être donnés à l'Agent à l'étape 2.

---

## Étape 1 : construire la règle de détection des dérives

**Durée : 20 min**

Une alerte « boîte noire » n'est pas utilisable par un chef de projet. Il faut une règle explicite, que l'IA devra suivre et justifier.

### À faire

1. Définissez ce qu'est une tâche « en retard » et une tâche « à risque ». Exemple :

   ```text
   En retard : date de fin prévue dépassée et avancement < 100 %.
   À risque  : moins de 5 jours ouvrés avant la date de fin prévue et avancement < 80 %.
   ```

2. Définissez la règle de propagation sur les dépendances : si une tâche est en retard, toute tâche qui en dépend est automatiquement considérée à risque.
3. Décidez du format de la justification attendue, par exemple :

   ```text
   Tâche               : Rédaction du cahier des charges
   Statut              : EN RETARD
   Fin prévue          : 12/09, avancement 70 %
   Impact              : bloque le démarrage du développement (dépendance directe)
   Retard estimé       : 4 jours sur la date de livraison finale
   ```

**Résultat attendu :** une règle de détection validée, avec sa logique de propagation et le format de justification.

---

## Étape 2 : construire l'application

**Durée : 60 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape avant de passer à la suivante.

### Les sept prompts

1. **Import du planning**
   > « Crée une application web avec un import de fichier CSV ou Excel contenant, par tâche : nom, responsable, date de début prévue, date de fin prévue, avancement en pourcentage, et une liste de tâches dont elle dépend. »

2. **Nettoyage et contrôle de qualité**
   > « Ajoute un contrôle de qualité de l'import : dates incohérentes (fin avant début), avancement hors de 0-100 %, dépendance vers une tâche inexistante, avec un rapport des lignes à corriger. »

3. **Détection des tâches en retard ou à risque**
   > « En te basant sur la règle suivante [colle ta règle de l'étape 1], détecte les tâches en retard et les tâches à risque. »

4. **Propagation sur les dépendances**
   > « Propage le statut à risque aux tâches qui dépendent d'une tâche en retard, et calcule un retard estimé sur la date de livraison finale du projet. »

5. **Justification détaillée**
   > « Pour chaque tâche en retard ou à risque, rédige une justification dans le format suivant [colle ton format de l'étape 1]. »

6. **Tableau de bord de suivi**
   > « Crée un tableau de bord qui liste les tâches par statut (à jour, à risque, en retard), avec le détail de chaque tâche accessible en un clic. »

7. **Compte rendu automatique**
   > « Génère un compte rendu hebdomadaire en français, résumant l'avancement global, les tâches à risque ou en retard, et l'impact estimé sur la date de livraison, prêt à être relu avant envoi. »

### Méthode

- Un prompt → un test → une correction si besoin → on passe au suivant.
- Si l'Agent produit une erreur, ne cumulez pas les instructions : demandez la correction avant de continuer (voir le module 6 du programme pour la méthode de débogage).
- Utilisez les **Secrets** de Replit pour toute clé d'API, jamais le code ni le chat.

**Résultat attendu :** une application fonctionnelle, accessible en Preview, qui va de l'import du planning jusqu'au compte rendu automatique.

---

## Étape 3 : tester sur des cas piégés

**Durée : 30 min**

Préparez ou demandez au formateur un planning avec des cas volontairement difficiles :

- une tâche en retard qui bloque deux autres tâches en cascade ;
- une tâche avec une dépendance circulaire (A dépend de B, B dépend de A) ;
- une tâche à 0 % d'avancement mais dont la date de fin prévue n'est pas encore dépassée (ne doit pas être signalée à tort) ;
- une tâche sans aucune dépendance, très en retard, mais sans impact sur les autres tâches.

### À faire

1. Chargez le planning dans l'application.
2. Notez dans un tableau : tâche testée → statut obtenu → impact estimé → justification produite → cohérente ou non.
3. Pour la dépendance circulaire : vérifiez que l'application la signale plutôt que de produire un résultat incohérent ou de boucler.
4. Demandez à l'Agent de corriger tout comportement incohérent repéré.

**Résultat attendu :** un tableau de tests avec les résultats, à conserver pour la documentation finale.

---

## Étape 4 : ajouter la validation humaine

**Durée : 15 min**

Le compte rendu généré par l'IA ne doit jamais partir directement au client ou à la direction sans relecture.

### À faire

Demandez à l'Agent :
> « Affiche le compte rendu généré dans un écran de relecture, avec un statut Brouillon / Validé / Envoyé, un champ pour modifier le texte avant validation, et la date et le nom de la personne qui valide. Le compte rendu ne doit être marqué comme prêt à diffuser qu'après validation humaine. »

**Résultat attendu :** un écran où le chef de projet relit, modifie si besoin, valide, et où le statut du compte rendu est visible.

---

## Étape 5 : discuter fiabilité et limites de l'estimation

**Durée : 20 min**

Cette étape est une discussion, pas une construction. Prenez des notes : elles alimenteront la documentation finale.

### Points à aborder

- **Fiabilité de l'estimation d'impact** : estimer un retard sur la date finale à partir de quelques règles simples reste approximatif. Quelles limites avez-vous observées sur vos cas de test ?
- **Dépendances incomplètes** : que se passe-t-il si toutes les dépendances réelles entre tâches n'ont pas été saisies dans le planning ? L'application peut-elle le détecter ?
- **Compte rendu automatique** : quels risques y a-t-il à envoyer un texte généré par l'IA sans relecture (ton, exactitude, information sensible) ?
- **Rôle de l'IA** : reformulez en une phrase le principe du lab — *l'IA détecte et rédige un brouillon, le chef de projet valide avant diffusion*.

**Résultat attendu :** des notes de discussion sur la fiabilité de l'estimation et les limites du compte rendu automatique.

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
# Lab Project Management — Suivi d'avancement et détection de dérives

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Les grandes étapes techniques : import, contrôle qualité, détection, propagation, compte rendu]

## Règle de détection des dérives
[Votre règle de l'étape 1]

## Tests réalisés
[Votre tableau de l'étape 3]

## Validation humaine
[Comment la relecture du chef de projet a été intégrée]

## Fiabilité et limites
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
git add LAB5_PROJECT_MANAGEMENT.md
git commit -m "Lab Project Management : suivi d'avancement et détection de dérives"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

Si le dépôt existe déjà, remplacez les trois premières lignes par :

```bash
git add LAB5_PROJECT_MANAGEMENT.md
git commit -m "Ajout du lab Project Management"
git push
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour aller plus loin sur les Secrets, l'authentification et la traçabilité.
