# Lab 6 - Audit : assistant de contrôle et d'échantillonnage

> Module du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** Un auditeur interne doit vérifier la conformité d'un grand nombre de transactions ou de dossiers, mais ne peut pas tout contrôler manuellement.

**Objectif.** Construire une application qui propose un échantillon représentatif à contrôler, avec la **méthode utilisée expliquée**, signale les anomalies statistiques, et génère une fiche de constat par anomalie que l'auditeur valide ou écarte.

**Vous allez construire**
- un import des transactions ou dossiers à auditer ;
- un tirage d'échantillon avec la méthode justifiée ;
- une détection d'anomalies statistiques (valeurs aberrantes, écarts aux procédures) ;
- une fiche de constat par anomalie, à valider ou écarter.

**Vous allez apprendre**
- à faire justifier une méthode d'échantillonnage plutôt qu'à obtenir une liste sans explication ;
- à distinguer une anomalie statistique d'une non-conformité réelle, et à documenter les limites d'un contrôle assisté par IA.

**Livrable final** : application déployée + cahier des charges + architecture + jeux de tests + résultats + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Définir le processus métier](#étape-0--définir-le-processus-métier) | Schéma du processus + jeu de données de référence |
| 1 | [Construire la méthode d'échantillonnage](#étape-1--construire-la-méthode-déchantillonnage) | Méthode validée |
| 2 | [Construire l'application](#étape-2--construire-lapplication) | Application fonctionnelle |
| 3 | [Tester sur des cas piégés](#étape-3--tester-sur-des-cas-piégés) | Jeux de tests + résultats |
| 4 | [Ajouter la décision humaine](#étape-4--ajouter-la-décision-humaine) | Écran de validation des constats |
| 5 | [Discuter fiabilité et limites du contrôle assisté](#étape-5--discuter-fiabilité-et-limites-du-contrôle-assisté) | Notes de discussion |
| 6 | [Documenter](#étape-6--documenter) | Dossier final du projet |

---

## Étape 0 : définir le processus métier

**Durée : 20 min**

Avant d'ouvrir Replit, formalisez le flux sur papier ou dans un document.

```text
Transactions ou dossiers
 ↓
Tirage de l'échantillon
 ↓
Contrôle des règles de conformité
 ↓
Détection des anomalies statistiques
 ↓
Fiche de constat par anomalie
 ↓
Validation humaine
 ↓
Rapport d'audit
```

### À faire

1. Constituez un jeu fictif d'une centaine de transactions (montant, date, service émetteur, type de dépense, pièce justificative présente ou non).
2. Notez ce schéma en haut de votre futur fichier `README.md` de projet : il servira de référence pendant toute la construction.
3. Identifiez qui utilisera l'application (l'auditeur interne) et ce qu'il attend de chaque écran.

**Résultat attendu :** un schéma du processus et un jeu de données de référence, prêts à être donnés à l'Agent à l'étape 2.

---

## Étape 1 : construire la méthode d'échantillonnage

**Durée : 20 min**

Un échantillon « boîte noire » n'est pas défendable devant un audité. Il faut une méthode explicite, que l'IA devra suivre et justifier.

### À faire

1. Choisissez une méthode d'échantillonnage simple et documentée. Exemple :

   ```text
   Échantillon = 10 % des transactions, avec sur-représentation systématique
   des transactions de montant supérieur à 5 000 € et de celles sans
   pièce justificative.
   ```

2. Définissez 2 ou 3 règles de conformité que chaque transaction échantillonnée doit respecter (ex. pièce justificative obligatoire au-delà d'un montant, double validation au-delà d'un autre seuil).
3. Décidez du format de la fiche de constat attendue, par exemple :

   ```text
   Transaction         : #4821
   Motif de sélection  : montant élevé (7 200 €)
   Règle vérifiée      : pièce justificative obligatoire au-delà de 5 000 €
   Constat             : pièce justificative absente
   Niveau de risque    : élevé
   ```

**Résultat attendu :** une méthode d'échantillonnage validée, avec les règles de conformité et le format de constat.

---

## Étape 2 : construire l'application

**Durée : 60 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape avant de passer à la suivante.

### Les sept prompts

1. **Import des transactions**
   > « Crée une application web avec un import de fichier CSV ou Excel contenant, par transaction : identifiant, montant, date, service émetteur, type de dépense, présence d'une pièce justificative. »

2. **Nettoyage et contrôle de qualité**
   > « Ajoute un contrôle de qualité de l'import : montants manquants ou négatifs, dates invalides, doublons de transaction, avec un rapport des lignes à corriger. »

3. **Tirage de l'échantillon**
   > « En te basant sur la méthode suivante [colle ta méthode de l'étape 1], tire un échantillon de transactions à contrôler et explique pour chacune son motif de sélection. »

4. **Contrôle des règles de conformité**
   > « Pour chaque transaction de l'échantillon, vérifie les règles de conformité suivantes [colle tes règles de l'étape 1] et indique si elles sont respectées. »

5. **Détection d'anomalies statistiques**
   > « En dehors de l'échantillon, détecte les transactions dont le montant est statistiquement inhabituel par rapport aux transactions du même type de dépense. »

6. **Fiches de constat**
   > « Pour chaque non-conformité ou anomalie détectée, génère une fiche de constat dans le format suivant [colle ton format de l'étape 1]. »

7. **Rapport d'audit et export**
   > « Crée un tableau de bord qui liste toutes les fiches de constat par niveau de risque, avec un export du rapport complet au format CSV ou Excel. »

### Méthode

- Un prompt → un test → une correction si besoin → on passe au suivant.
- Si l'Agent produit une erreur, ne cumulez pas les instructions : demandez la correction avant de continuer (voir le module 6 du programme pour la méthode de débogage).
- Utilisez les **Secrets** de Replit pour toute clé d'API, jamais le code ni le chat.

**Résultat attendu :** une application fonctionnelle, accessible en Preview, qui va de l'import des transactions jusqu'au rapport d'audit.

---

## Étape 3 : tester sur des cas piégés

**Durée : 30 min**

Préparez ou demandez au formateur un jeu de données avec des cas volontairement difficiles :

- une transaction de montant très élevé mais parfaitement conforme (pièce justificative présente, double validation faite) ;
- une transaction de faible montant mais sans aucune pièce justificative ;
- deux transactions presque identiques, dont une seule dépasse le seuil de contrôle, pour vérifier que la règle s'applique au bon moment ;
- une transaction avec une date future ou incohérente.

### À faire

1. Chargez le jeu de données dans l'application.
2. Notez dans un tableau : transaction testée → sélectionnée ou non → constat produit → cohérent ou non.
3. Pour la transaction de montant élevé mais conforme : vérifiez qu'elle est bien sélectionnée (sur-représentation) mais qu'aucune fiche de constat erronée n'est générée.
4. Demandez à l'Agent de corriger tout comportement incohérent repéré.

**Résultat attendu :** un tableau de tests avec les résultats, à conserver pour la documentation finale.

---

## Étape 4 : ajouter la décision humaine

**Durée : 15 min**

Un constat généré par l'IA n'est qu'une proposition. L'auditeur doit pouvoir le confirmer ou l'écarter.

### À faire

Demandez à l'Agent :
> « Ajoute pour chaque fiche de constat une zone de décision de l'auditeur : Confirmer / Écarter / À approfondir, avec un champ de commentaire libre et la date de la décision. Seuls les constats confirmés doivent apparaître dans le rapport d'audit final. »

**Résultat attendu :** un écran où l'auditeur peut confirmer, écarter ou approfondir chaque constat avant qu'il n'entre dans le rapport final.

---

## Étape 5 : discuter fiabilité et limites du contrôle assisté

**Durée : 20 min**

Cette étape est une discussion, pas une construction. Prenez des notes : elles alimenteront la documentation finale.

### Points à aborder

- **Fiabilité de l'échantillonnage** : une méthode simple peut sur- ou sous-représenter certains types de transactions. Quelles limites avez-vous observées sur vos cas de test ?
- **Anomalie statistique contre non-conformité réelle** : un montant inhabituel n'est pas toujours une fraude ou une erreur. Comment l'application évite-t-elle de l'affirmer à tort ?
- **Traçabilité** : pourquoi est-il essentiel, en audit, de pouvoir justifier chaque sélection et chaque constat, y compris ceux écartés par l'auditeur ?
- **Rôle de l'IA** : reformulez en une phrase le principe du lab — *l'IA oriente le contrôle, elle ne certifie rien : l'auditeur confirme*.

**Résultat attendu :** des notes de discussion sur la fiabilité de la méthode et les limites du contrôle assisté par IA.

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
# Lab Audit — Assistant de contrôle et d'échantillonnage

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Les grandes étapes techniques : import, contrôle qualité, échantillonnage, détection, rapport]

## Méthode d'échantillonnage
[Votre méthode de l'étape 1]

## Tests réalisés
[Votre tableau de l'étape 3]

## Décision humaine
[Comment la validation de l'auditeur a été intégrée]

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
git add LAB6_AUDIT.md
git commit -m "Lab Audit : assistant de contrôle et d'échantillonnage"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

Si le dépôt existe déjà, remplacez les trois premières lignes par :

```bash
git add LAB6_AUDIT.md
git commit -m "Ajout du lab Audit"
git push
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour aller plus loin sur les Secrets, l'authentification et la traçabilité.
