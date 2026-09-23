# Lab 4 - Supply Chain : suivi et alerte de rupture de stock

> Module du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** Un gestionnaire logistique suit les stocks de plusieurs entrepôts. Sans outil, il découvre souvent une rupture au moment où elle affecte déjà la production ou les ventes.

**Objectif.** Construire une application qui surveille les niveaux de stock, calcule un seuil de réapprovisionnement par produit et **alerte avant la rupture**, avec une quantité de commande suggérée et justifiée. La décision de commander reste au gestionnaire.

**Vous allez construire**
- un import des stocks et de l'historique de consommation ;
- un calcul de seuil de réapprovisionnement par produit ;
- une liste des produits à risque, classés par urgence, avec justification ;
- une quantité de commande suggérée et un export du plan de réapprovisionnement.

**Vous allez apprendre**
- à faire expliquer un calcul par l'IA plutôt qu'à obtenir un résultat opaque ;
- à distinguer une alerte fiable d'une fausse alerte, et à en tirer les limites d'une prévision simple.

**Livrable final** : application déployée + cahier des charges + architecture + jeux de tests + résultats + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Définir le processus métier](#étape-0--définir-le-processus-métier) | Schéma du processus + données de référence |
| 1 | [Construire la règle de seuil](#étape-1--construire-la-règle-de-seuil) | Règle de seuil validée |
| 2 | [Construire l'application](#étape-2--construire-lapplication) | Application fonctionnelle |
| 3 | [Tester sur des cas piégés](#étape-3--tester-sur-des-cas-piégés) | Jeux de tests + résultats |
| 4 | [Ajouter la décision humaine](#étape-4--ajouter-la-décision-humaine) | Écran de décision d'achat |
| 5 | [Discuter fiabilité et limites de la prévision](#étape-5--discuter-fiabilité-et-limites-de-la-prévision) | Notes de discussion |
| 6 | [Documenter](#étape-6--documenter) | Dossier final du projet |

---

## Étape 0 : définir le processus métier

**Durée : 20 min**

Avant d'ouvrir Replit, formalisez le flux sur papier ou dans un document.

```text
Stocks + historique de consommation
 ↓
Calcul du seuil de réapprovisionnement
 ↓
Comparaison stock actuel / seuil
 ↓
Détection des produits à risque
 ↓
Quantité de commande suggérée
 ↓
Justification
 ↓
Validation humaine
 ↓
Plan de réapprovisionnement
```

### À faire

1. Listez une dizaine de produits fictifs avec : stock actuel, consommation moyenne par semaine, délai de livraison fournisseur, et une consommation qui varie (saisonnalité, pics ponctuels).
2. Notez ce schéma en haut de votre futur fichier `README.md` de projet : il servira de référence pendant toute la construction.
3. Identifiez qui utilisera l'application (le gestionnaire logistique) et ce qu'il attend de chaque écran.

**Résultat attendu :** un schéma du processus et un jeu de données de référence, prêts à être donnés à l'Agent à l'étape 2.

---

## Étape 1 : construire la règle de seuil

**Durée : 20 min**

Une alerte « boîte noire » n'est pas utilisable par un gestionnaire. Il faut une règle explicite, que l'IA devra suivre et justifier.

### À faire

1. Définissez la règle de seuil de réapprovisionnement. Exemple simple :

   ```text
   Seuil = (consommation moyenne par jour × délai de livraison fournisseur) + stock de sécurité
   ```

2. Choisissez un stock de sécurité par produit ou par famille de produits (ex. 20 % de la consommation du délai de livraison).
3. Décidez du format de la justification attendue, par exemple :

   ```text
   Produit : Cartouches d'encre noire
   Stock actuel        : 40 unités
   Consommation/semaine: 25 unités
   Délai fournisseur   : 2 semaines
   Seuil calculé       : 50 + 10 (sécurité) = 60 unités
   Statut              : SOUS LE SEUIL — commander sous 3 jours
   Quantité suggérée   : 80 unités (couvre 3 semaines)
   ```

**Résultat attendu :** une règle de seuil validée, avec son mode de calcul et le format de justification.

---

## Étape 2 : construire l'application

**Durée : 60 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape avant de passer à la suivante.

### Les sept prompts

1. **Import des stocks et de la consommation**
   > « Crée une application web avec un import de fichier CSV ou Excel contenant, par produit : stock actuel, consommation par semaine, délai de livraison fournisseur. »

2. **Nettoyage et contrôle de qualité**
   > « Ajoute un contrôle de qualité de l'import : valeurs manquantes, stocks négatifs, doublons de produits, avec un rapport des lignes rejetées. »

3. **Calcul du seuil de réapprovisionnement**
   > « En te basant sur la règle suivante [colle ta règle de l'étape 1], calcule le seuil de réapprovisionnement pour chaque produit. »

4. **Détection des produits à risque**
   > « Compare le stock actuel de chaque produit à son seuil, et classe les produits en trois statuts : au-dessus du seuil, proche du seuil, sous le seuil. »

5. **Quantité suggérée et justification**
   > « Pour chaque produit sous le seuil ou proche du seuil, propose une quantité de commande et rédige une justification dans le format suivant [colle ton format de l'étape 1]. »

6. **Tableau de bord par urgence**
   > « Crée un tableau de bord qui liste les produits à risque du plus urgent au moins urgent, avec le détail de chaque produit accessible en un clic. »

7. **Export du plan de réapprovisionnement**
   > « Ajoute un bouton d'export du plan de réapprovisionnement (produit, quantité suggérée, justification) au format CSV ou Excel. »

### Méthode

- Un prompt → un test → une correction si besoin → on passe au suivant.
- Si l'Agent produit une erreur, ne cumulez pas les instructions : demandez la correction avant de continuer (voir le module 6 du programme pour la méthode de débogage).
- Utilisez les **Secrets** de Replit pour toute clé d'API, jamais le code ni le chat.

**Résultat attendu :** une application fonctionnelle, accessible en Preview, qui va de l'import des stocks jusqu'à l'export du plan de réapprovisionnement.

---

## Étape 3 : tester sur des cas piégés

**Durée : 30 min**

Préparez ou demandez au formateur un jeu de données avec des cas volontairement difficiles :

- un produit avec une consommation très irrégulière (pics ponctuels) ;
- un produit avec un délai fournisseur inhabituellement long ;
- un produit dont le stock est à zéro ;
- deux produits presque identiques, avec une seule donnée différente (le délai fournisseur), pour vérifier que la règle réagit bien à ce changement.

### À faire

1. Chargez le jeu de données dans l'application.
2. Notez dans un tableau : produit testé → statut obtenu → quantité suggérée → justification produite → cohérente ou non.
3. Pour les deux produits presque identiques : vérifiez que seul le délai fournisseur explique l'écart de seuil. Si un autre facteur semble jouer sans raison, c'est un signal à corriger ou à documenter.
4. Demandez à l'Agent de corriger tout comportement incohérent repéré.

**Résultat attendu :** un tableau de tests avec les résultats, à conserver pour la documentation finale.

---

## Étape 4 : ajouter la décision humaine

**Durée : 15 min**

La quantité suggérée par l'IA n'est qu'une aide. Le gestionnaire doit pouvoir décider et garder la main sur la commande.

### À faire

Demandez à l'Agent :
> « Ajoute pour chaque produit à risque une zone de décision du gestionnaire : Commander / Reporter / Ignorer, avec un champ de quantité modifiable, un commentaire libre et la date de la décision. Cette décision doit apparaître dans le tableau de bord à côté de la suggestion de l'IA. »

**Résultat attendu :** un écran où le gestionnaire peut décider, ajuster la quantité, commenter, et voir sa décision affichée à côté de la suggestion de l'IA.

---

## Étape 5 : discuter fiabilité et limites de la prévision

**Durée : 20 min**

Cette étape est une discussion, pas une construction. Prenez des notes : elles alimenteront la documentation finale.

### Points à aborder

- **Fiabilité de la règle** : une moyenne de consommation simple capture mal les pics ponctuels ou la saisonnalité. Quelles limites avez-vous observées sur vos cas de test ?
- **Fausses alertes et alertes manquées** : que se passe-t-il si le seuil est mal calibré ? Quel est le coût d'une fausse alerte (sur-stockage) comparé à celui d'une alerte manquée (rupture) ?
- **Données fournisseur** : le délai de livraison réel varie souvent. Comment l'application pourrait-elle être mise à jour si ce délai change ?
- **Rôle de l'IA** : reformulez en une phrase le principe du lab — *l'IA alerte et suggère, le gestionnaire décide de la commande*.

**Résultat attendu :** des notes de discussion sur la fiabilité de la règle et les limites de la prévision.

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
# Lab Supply Chain — Suivi et alerte de rupture de stock

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Les grandes étapes techniques : import, contrôle qualité, seuil, détection, export]

## Règle de seuil
[Votre règle de l'étape 1]

## Tests réalisés
[Votre tableau de l'étape 3]

## Décision humaine
[Comment la validation du gestionnaire a été intégrée]

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
git add LAB4_SUPPLY_CHAIN.md
git commit -m "Lab Supply Chain : suivi et alerte de rupture de stock"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

Si le dépôt existe déjà, remplacez les trois premières lignes par :

```bash
git add LAB4_SUPPLY_CHAIN.md
git commit -m "Ajout du lab Supply Chain"
git push
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour aller plus loin sur les Secrets, l'authentification et la traçabilité.
