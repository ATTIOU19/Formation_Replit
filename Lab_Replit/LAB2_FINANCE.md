# Lab 2 — Finance : assistant d'analyse comptable

> Module 4 du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

## Objectif du lab

**Scénario.** En fin de période, le comptable doit trier des dizaines de transactions, repérer les erreurs et rapprocher le relevé bancaire. Ce travail est répétitif et chronophage.

**Objectif.** Construire un assistant qui prépare ce travail, pour que le comptable se concentre sur la vérification et l'analyse plutôt que sur la saisie.

**Vous allez construire**
- un import et un nettoyage des données de transactions ;
- une classification automatique par compte comptable ;
- une détection d'anomalies et un rapprochement bancaire simplifié ;
- un tableau de bord et un rapport automatique.

**Vous allez apprendre**
- à construire un pipeline de données fiable, étape par étape ;
- à contrôler la qualité des résultats produits par l'IA avant de leur faire confiance.

**Livrable final** : application déployée + jeux de tests + résultats + limites identifiées.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Formaliser le pipeline](#étape-0--formaliser-le-pipeline) | Schéma du pipeline |
| 1 | [Import, nettoyage et contrôle qualité](#étape-1--import-nettoyage-et-contrôle-qualité) | Module d'import propre |
| 2 | [Classification par compte comptable](#étape-2--classification-par-compte-comptable) | Classification avec niveau de confiance |
| 3 | [Anomalies et rapprochement bancaire](#étape-3--anomalies-et-rapprochement-bancaire) | Rapport d'anomalies et d'écarts |
| 4 | [Analyse et tableau de bord](#étape-4--analyse-et-tableau-de-bord) | Dashboard |
| 5 | [Rapport automatique et export Excel](#étape-5--rapport-automatique-et-export-excel) | Rapport + export Excel |
| 6 | [Tests et discussion](#étape-6--tests-et-discussion) | Jeux de tests + résultats + limites |

---

## Étape 0 : formaliser le pipeline

**Durée : 15 min**

Avant d'ouvrir Replit, formalisez le flux de traitement sur papier ou dans un document.

```text
Transactions
     ↓
Nettoyage
     ↓
Contrôle qualité
     ↓
Classification
     ↓
Détection d'anomalies
     ↓
Analyse
     ↓
Dashboard
     ↓
Rapport automatique
```

### À faire

1. Rassemblez ou préparez un jeu de données fictif : un relevé bancaire, une liste de factures et un plan comptable simplifié (ex. Loyer, Fournitures, Salaires, Honoraires, Divers).
2. Notez ce schéma en haut du futur `README.md` du projet : il guidera vos prompts à l'étape 2.
3. Identifiez qui utilisera l'application (le comptable) et ce qu'il doit pouvoir vérifier à chaque étape.

**Résultat attendu :** un schéma du pipeline et un jeu de données prêts à être donnés à l'Agent.

---

## Étape 1 : import, nettoyage et contrôle qualité

**Durée : 30 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape.

### À faire

> **Prompt 1** — « Crée une application web avec un import de fichier de transactions au format CSV ou Excel (colonnes : date, libellé, montant, compte bancaire). »

> **Prompt 2** — « Ajoute le nettoyage automatique des données importées : harmonise les formats de date et de montant, et signale les valeurs manquantes ou mal formées sans les supprimer silencieusement. »

> **Prompt 3** — « Affiche un rapport de qualité des données : nombre de lignes importées, nombre de lignes rejetées et pourquoi, nombre de champs vides par colonne. »

### Points de vigilance

- Vérifiez que les montants avec virgule et point décimal sont bien reconnus.
- Vérifiez que les dates dans des formats différents (JJ/MM/AAAA, AAAA-MM-JJ) sont bien harmonisées.

**Résultat attendu :** un module d'import qui accepte le fichier, nettoie les données et affiche un rapport de qualité clair.

---

## Étape 2 : classification par compte comptable

**Durée : 30 min**

### À faire

> **Prompt** — « En te basant sur ce plan comptable simplifié [colle ton plan comptable de l'étape 0], attribue automatiquement un compte à chaque transaction importée. Indique aussi un niveau de confiance (élevé, moyen, faible) pour chaque attribution, et liste séparément les cas douteux à vérifier par un humain. »

### Vérification

1. Contrôlez une dizaine de lignes à la main : la classification est-elle plausible ?
2. Regardez la liste des cas douteux : sont-ils vraiment ambigus, ou l'IA aurait-elle pu faire mieux ? Si besoin, précisez votre plan comptable et redemandez.

**Résultat attendu :** chaque transaction a un compte proposé, un niveau de confiance, et les cas douteux sont isolés.

---

## Étape 3 : anomalies et rapprochement bancaire

**Durée : 40 min**

### À faire

> **Prompt 1** — « Détecte dans les transactions importées : les doublons, les montants inhabituels par rapport à l'historique, les dates incohérentes (ex. dans le futur), et les transactions sans pièce justificative associée. Liste chaque anomalie avec son motif. »

> **Prompt 2** — « Ajoute un rapprochement bancaire simplifié : mets en correspondance les transactions du relevé bancaire avec la liste des factures, et affiche la liste des écarts (transactions sans facture, factures sans transaction). »

### Points de vigilance

- Une anomalie détectée n'est pas forcément une erreur : c'est une alerte à vérifier par le comptable.
- Le rapprochement doit rester lisible même s'il ne trouve pas 100 % de correspondances.

**Résultat attendu :** un rapport listant les anomalies et les écarts de rapprochement, avec leur motif.

---

## Étape 4 : analyse et tableau de bord

**Durée : 30 min**

### À faire

> **Prompt** — « Crée un tableau de bord avec : le total des dépenses par compte comptable, la moyenne mensuelle, la répartition des dépenses par catégorie sous forme de graphique, et l'évolution des dépenses dans le temps. »

**Résultat attendu :** un dashboard visuel avec les indicateurs clés du comptable, mis à jour à chaque import.

---

## Étape 5 : rapport automatique et export Excel

**Durée : 15 min**

### À faire

> **Prompt** — « Génère un récapitulatif de clôture : liste des tâches à faire, liste des anomalies à traiter, liste des éléments à vérifier. Ajoute un bouton d'export de ce récapitulatif et des transactions classifiées au format Excel. »

**Résultat attendu :** une checklist de clôture générée automatiquement, exportable en Excel.

---

## Étape 6 : tests et discussion

**Durée : 20 min**

### À faire

1. Modifiez volontairement votre fichier de transactions pour y ajouter :
   - un doublon exact d'une ligne existante ;
   - un montant clairement aberrant (ex. 50 000 € sur une dépense habituellement à 50 €).
2. Réimportez le fichier et vérifiez que les deux anomalies sont bien détectées et expliquées.
3. Si l'une des deux passe inaperçue, demandez à l'Agent d'ajuster la détection.

### Discussion à mener

- **Le comptable vérifie toujours** : une opération peut être mal classée par l'IA. À quel moment de son travail doit-il impérativement contrôler ?
- **Confidentialité** : seules des données fictives ont été utilisées ici. Que faudrait-il changer avant d'utiliser de vraies données de l'entreprise ?
- **Traçabilité** : comment retrouver, plus tard, qui (l'IA ou un humain) a validé une classification ou corrigé une anomalie ?

**Résultat attendu :** un tableau de tests avec les deux anomalies volontaires et leur détection, plus des notes de discussion sur les limites.

---

## Documenter le lab

Rassemblez tout ce qui a été produit dans un dossier de projet clair, puis déployez l'application avec le bouton **Deploy** de Replit.

### Modèle de fiche projet

```markdown
# Lab Finance — Assistant d'analyse comptable

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture (pipeline)
[Import, nettoyage, classification, anomalies, dashboard, rapport]

## Plan comptable utilisé
[Votre plan comptable de l'étape 0]

## Tests réalisés
[Doublon et montant aberrant : détectés ou non, corrections apportées]

## Discussion
[Vérification humaine, confidentialité, traçabilité]

## Limites identifiées
[Ce que l'application ne fait pas ou ne fait pas bien]

## Lien vers l'application déployée
[URL Replit]
```

**Résultat attendu (livrable final du lab)** : application déployée + jeux de tests + résultats + limites.

---

## Pousser ce lab sur GitHub

```bash
git add LAB2_FINANCE.md
git commit -m "Lab 2 Finance : assistant d'analyse comptable"
git push
```

Si c'est le premier fichier du dépôt :

```bash
git init
git add LAB2_FINANCE.md
git commit -m "Lab 2 Finance : assistant d'analyse comptable"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour approfondir la protection des données financières et la traçabilité.
