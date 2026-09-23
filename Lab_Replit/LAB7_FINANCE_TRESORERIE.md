# Lab 7 - Finance avancé : assistant de prévision de trésorerie

> Module du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** Un contrôleur de gestion doit anticiper les tensions de trésorerie à venir en croisant les encaissements attendus des clients et les échéances de paiement des fournisseurs.

**Objectif.** Construire une application qui projette la trésorerie sur plusieurs semaines, détecte les semaines à risque de découvert, et propose des actions correctives **classées par impact**, avec une simulation « et si » pour tester des hypothèses.

**Vous allez construire**
- un import des factures clients (encaissements attendus) et fournisseurs (paiements prévus) ;
- un prévisionnel de trésorerie semaine par semaine ;
- une détection des semaines à risque, avec justification ;
- des actions correctives suggérées et une simulation de scénario.

**Vous allez apprendre**
- à faire construire une projection simple et vérifiable plutôt qu'un chiffre final non expliqué ;
- à tester des hypothèses (« et si un client paie en retard ? ») et à en mesurer l'impact avant de décider.

**Livrable final** : application déployée + cahier des charges + architecture + jeux de tests + résultats + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Définir le processus métier](#étape-0--définir-le-processus-métier) | Schéma du processus + données de référence |
| 1 | [Construire la règle de projection](#étape-1--construire-la-règle-de-projection) | Règle de projection validée |
| 2 | [Construire l'application](#étape-2--construire-lapplication) | Application fonctionnelle |
| 3 | [Tester sur des cas piégés](#étape-3--tester-sur-des-cas-piégés) | Jeux de tests + résultats |
| 4 | [Ajouter la décision humaine](#étape-4--ajouter-la-décision-humaine) | Écran de décision sur les actions |
| 5 | [Discuter fiabilité et limites de la prévision](#étape-5--discuter-fiabilité-et-limites-de-la-prévision) | Notes de discussion |
| 6 | [Documenter](#étape-6--documenter) | Dossier final du projet |

---

## Étape 0 : définir le processus métier

**Durée : 20 min**

Avant d'ouvrir Replit, formalisez le flux sur papier ou dans un document.

```text
Factures clients + factures fournisseurs
 ↓
Projection semaine par semaine
 ↓
Calcul du solde de trésorerie prévisionnel
 ↓
Détection des semaines à risque
 ↓
Actions correctives suggérées
 ↓
Validation humaine
 ↓
Prévisionnel validé
```

### À faire

1. Constituez un jeu fictif de 15 à 20 factures clients (montant, date d'échéance prévue, historique de retard du client) et autant de factures fournisseurs (montant, date de paiement prévue).
2. Fixez un solde de trésorerie de départ.
3. Notez ce schéma en haut de votre futur fichier `README.md` de projet : il servira de référence pendant toute la construction.
4. Identifiez qui utilisera l'application (le contrôleur de gestion) et ce qu'il attend de chaque écran.

**Résultat attendu :** un schéma du processus et un jeu de données de référence, prêts à être donnés à l'Agent à l'étape 2.

---

## Étape 1 : construire la règle de projection

**Durée : 20 min**

Un prévisionnel « boîte noire » n'est pas utilisable par un contrôleur de gestion. Il faut une règle explicite, que l'IA devra suivre et justifier.

### À faire

1. Définissez la règle de calcul du solde prévisionnel semaine par semaine. Exemple :

   ```text
   Solde semaine N = Solde semaine N-1
                    + encaissements clients attendus en semaine N
                    - paiements fournisseurs prévus en semaine N
   ```

2. Définissez une règle d'ajustement du risque de retard client, par exemple à partir de son historique :

   ```text
   Si le client a déjà payé en retard : décaler l'encaissement attendu
   de son retard moyen observé, à titre de scénario prudent.
   ```

3. Décidez du format de la justification attendue pour une semaine à risque, par exemple :

   ```text
   Semaine             : 12/10 au 18/10
   Solde prévisionnel  : -3 200 €
   Cause principale    : paiement fournisseur de 15 000 € le 14/10,
                         encaissement client de 8 000 € attendu mais
                         historiquement payé avec 10 jours de retard
   Seuil d'alerte       : solde négatif
   ```

**Résultat attendu :** une règle de projection validée, avec l'ajustement de risque et le format de justification.

---

## Étape 2 : construire l'application

**Durée : 60 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape avant de passer à la suivante.

### Les sept prompts

1. **Import des factures clients et fournisseurs**
   > « Crée une application web avec un import de fichier CSV ou Excel pour les factures clients (montant, échéance, historique de retard) et un autre pour les factures fournisseurs (montant, date de paiement prévue). »

2. **Nettoyage et contrôle de qualité**
   > « Ajoute un contrôle de qualité de l'import : montants manquants ou négatifs, dates invalides, doublons de facture, avec un rapport des lignes à corriger. »

3. **Projection semaine par semaine**
   > « En te basant sur la règle suivante [colle ta règle de l'étape 1], calcule le solde de trésorerie prévisionnel pour chaque semaine sur les 12 prochaines semaines, à partir du solde de départ [indique ton solde de l'étape 0]. »

4. **Ajustement du risque de retard client**
   > « Applique l'ajustement de risque suivant [colle ta règle de l'étape 1] aux encaissements des clients ayant un historique de retard, et calcule un scénario prudent en plus du scénario normal. »

5. **Détection des semaines à risque et justification**
   > « Identifie les semaines où le solde prévisionnel devient négatif dans le scénario prudent, et rédige une justification dans le format suivant [colle ton format de l'étape 1]. »

6. **Actions correctives suggérées**
   > « Pour chaque semaine à risque, propose une ou plusieurs actions correctives (relancer un client précis, décaler un paiement fournisseur précis) classées par impact sur le solde. »

7. **Tableau de bord et simulation « et si »**
   > « Crée un tableau de bord avec le graphique du solde prévisionnel sur 12 semaines, et une fonction permettant de simuler l'effet d'un changement (ex. un client paie 15 jours plus tard) sur la projection. »

### Méthode

- Un prompt → un test → une correction si besoin → on passe au suivant.
- Si l'Agent produit une erreur, ne cumulez pas les instructions : demandez la correction avant de continuer (voir le module 6 du programme pour la méthode de débogage).
- Utilisez les **Secrets** de Replit pour toute clé d'API, jamais le code ni le chat.

**Résultat attendu :** une application fonctionnelle, accessible en Preview, qui va de l'import des factures jusqu'à la simulation de scénario.

---

## Étape 3 : tester sur des cas piégés

**Durée : 30 min**

Préparez ou demandez au formateur un jeu de données avec des cas volontairement difficiles :

- un très gros encaissement client concentré sur une seule semaine, qui masque un risque les semaines suivantes ;
- un fournisseur payé en une seule fois alors que le montant pourrait être échelonné ;
- un client sans historique de retard (nouveau client), pour vérifier que l'application ne lui applique pas un ajustement de risque arbitraire ;
- deux semaines consécutives à risque, pour vérifier que l'application ne signale pas seulement la pire des deux.

### À faire

1. Chargez le jeu de données dans l'application.
2. Notez dans un tableau : semaine testée → solde obtenu → semaine signalée à risque ou non → justification produite → cohérente ou non.
3. Pour le nouveau client sans historique : vérifiez qu'aucun ajustement de risque injustifié ne lui est appliqué.
4. Demandez à l'Agent de corriger tout comportement incohérent repéré.

**Résultat attendu :** un tableau de tests avec les résultats, à conserver pour la documentation finale.

---

## Étape 4 : ajouter la décision humaine

**Durée : 15 min**

Les actions correctives suggérées par l'IA ne sont que des pistes. Le contrôleur de gestion doit décider de celles à engager.

### À faire

Demandez à l'Agent :
> « Ajoute pour chaque action corrective suggérée une zone de décision du contrôleur de gestion : Engager / Reporter / Ignorer, avec un champ de commentaire libre et la date de la décision. Recalcule automatiquement la projection de trésorerie si une action est marquée comme engagée. »

**Résultat attendu :** un écran où le contrôleur de gestion décide des actions à engager, avec une projection qui se met à jour en conséquence.

---

## Étape 5 : discuter fiabilité et limites de la prévision

**Durée : 20 min**

Cette étape est une discussion, pas une construction. Prenez des notes : elles alimenteront la documentation finale.

### Points à aborder

- **Fiabilité de la projection** : une projection sur 12 semaines repose sur des hypothèses (paiement à l'échéance, historique représentatif). Quelles limites avez-vous observées sur vos cas de test ?
- **Scénario prudent contre scénario optimiste** : pourquoi est-il utile de présenter les deux plutôt qu'un seul chiffre ?
- **Données sensibles** : les informations de trésorerie et les retards de paiement des clients sont des données financières sensibles. Quelles précautions prendre sur leur accès et leur conservation ?
- **Rôle de l'IA** : reformulez en une phrase le principe du lab - *l'IA projette et alerte, le contrôleur de gestion décide des actions à engager*.

**Résultat attendu :** des notes de discussion sur la fiabilité de la projection et les limites de la prévision.

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
# Lab Finance avancé — Assistant de prévision de trésorerie

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Les grandes étapes techniques : import, contrôle qualité, projection, détection, simulation]

## Règle de projection
[Votre règle de l'étape 1]

## Tests réalisés
[Votre tableau de l'étape 3]

## Décision humaine
[Comment la validation du contrôleur de gestion a été intégrée]

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
git add LAB7_FINANCE_TRESORERIE.md
git commit -m "Lab Finance avancé : assistant de prévision de trésorerie"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

Si le dépôt existe déjà, remplacez les trois premières lignes par :

```bash
git add LAB7_FINANCE_TRESORERIE.md
git commit -m "Ajout du lab Finance avancé"
git push
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour aller plus loin sur les Secrets, l'authentification et la traçabilité.
