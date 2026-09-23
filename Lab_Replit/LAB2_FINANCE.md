# Lab 2 — Facturation : application web de factures et de devis

> Module 4 du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Prérequis : aucun en programmation.

---

## Objectif du lab

**Scénario.** Une petite entreprise ou un indépendant doit créer des devis et des factures pour ses clients. Aujourd'hui, tout se fait à la main dans un tableur : les erreurs de calcul sont fréquentes, la numérotation n'est pas fiable et retrouver un document prend du temps.

**Objectif.** Construire une application web qui permet de créer, enregistrer, consulter et exporter des devis et des factures, avec un calcul automatique des totaux et une numérotation cohérente.

**Vous allez construire**

- un formulaire de création de devis et de facture ;
- un calcul automatique des totaux (HT, TVA, TTC) ;
- une base de données qui conserve les documents et les clients ;
- une page de liste avec recherche et filtres (devis / factures, payées / impayées) ;
- un export PDF ou Excel de chaque document.

**Vous allez apprendre**

- à construire une application web complète dans Replit, étape par étape ;
- à structurer une base de données simple pour des documents commerciaux ;
- à générer un export propre à partir d'un modèle ;
- à contrôler la qualité des résultats produits par l'IA avant de les utiliser auprès d'un vrai client.

**Livrable final** : application déployée + jeux de tests + résultats + limites identifiées.

---

## Comment utiliser les prompts de ce lab

Chaque prompt suit la même structure en quatre parties :

| Partie | Rôle |
|---|---|
| **Contexte** | Ce que l'Agent doit savoir du projet. |
| **Objectif** | Ce que l'on veut obtenir précisément. |
| **Contraintes** | Les règles à respecter (langue, format, sécurité). |
| **Format attendu** | Ce que doit produire l'Agent, concrètement. |

**Méthode de travail** : un prompt → un test → on avance. Ne passez au prompt suivant que lorsque le précédent fonctionne.

Pour copier un prompt, cliquez sur l'icône en haut à droite du bloc de code.

---

## Sommaire des étapes

| # | Étape | Ce que vous produisez |
|---|---|---|
| 0 | [Formaliser le besoin et le modèle de données](#étape-0--formaliser-le-besoin-et-le-modèle-de-données) | Schéma du flux et des tables |
| 1 | [Créer le formulaire de devis / facture](#étape-1--créer-le-formulaire-de-devis--facture) | Formulaire fonctionnel |
| 2 | [Calcul automatique des totaux](#étape-2--calcul-automatique-des-totaux) | Calcul HT, TVA, TTC fiable |
| 3 | [Enregistrement et base de données](#étape-3--enregistrement-et-base-de-données) | Documents conservés |
| 4 | [Liste, recherche et filtres](#étape-4--liste-recherche-et-filtres) | Page de liste utilisable |
| 5 | [Export PDF et Excel](#étape-5--export-pdf-et-excel) | Bouton d'export |
| 6 | [Tests et discussion](#étape-6--tests-et-discussion) | Jeux de tests + limites |

---

## Étape 0 : formaliser le besoin et le modèle de données

**Durée : 20 min**

Avant d'ouvrir Replit, formalisez le flux de création d'un document et les informations à stocker.

```text
Créer un document
     ↓
Choisir : devis ou facture
     ↓
Renseigner le client
     ↓
Ajouter les lignes (désignation, quantité, prix unitaire)
     ↓
Calcul automatique HT / TVA / TTC
     ↓
Enregistrer
     ↓
Consulter, exporter, marquer comme payé
```

### Les informations à stocker

**Clients**

- nom ou raison sociale
- adresse
- email
- numéro de TVA (facultatif)

**Documents (devis ou facture)**

- type : devis ou facture
- numéro (ex. DEV-2025-001 ou FAC-2025-001)
- date d'émission
- date de validité (pour un devis) ou date d'échéance (pour une facture)
- client associé
- statut : brouillon, envoyé, accepté, refusé, payé, impayé

**Lignes de document**

- désignation
- quantité
- prix unitaire HT
- taux de TVA
- total de la ligne HT et TTC

### À faire

1. Préparez un jeu de données fictif : deux ou trois clients (nom, adresse, email) et un jeu de lignes de test (ex. « Prestation de conseil — 2 h — 80 € HT — TVA 20 % »).
2. Notez ce schéma en haut du futur `README.md` du projet : il guidera vos prompts à l'étape 1.
3. Identifiez les règles métier : numérotation automatique, calcul de la TVA, mentions obligatoires sur une facture.

**Résultat attendu :** un schéma du flux, un modèle de données écrit et un jeu de données prêt à être donné à l'Agent.

---

## Étape 1 : créer le formulaire de devis / facture

**Durée : 30 min**

Ouvrez Replit, créez un nouveau projet, puis donnez vos instructions à l'Agent **une par une**. Testez après chaque étape.

### Prompt 1.1 — Page d'accueil

```text
Contexte : Je construis une application web de facturation pour une petite entreprise. Je débute le projet dans Replit.

Objectif : Créer une page d'accueil qui propose deux actions claires : créer un nouveau devis ou créer une nouvelle facture.

Contraintes :
- Interface en français.
- Design simple, lisible, adapté à un usage professionnel.
- Ne pas encore créer de base de données à cette étape.

Format attendu : une page d'accueil avec un titre, une courte phrase de présentation, et deux boutons : "Nouveau devis" et "Nouvelle facture".
```

### Prompt 1.2 — Formulaire de création

```text
Contexte : L'application de facturation a une page d'accueil avec deux boutons. Je veux maintenant le formulaire de création d'un document.

Objectif : Créer un formulaire qui permet de saisir un devis ou une facture.

Contraintes :
- Le formulaire doit contenir : un choix "devis" ou "facture", les informations du client (nom, adresse, email), la date d'émission, la date de validité (devis) ou d'échéance (facture).
- Le formulaire doit contenir une zone pour ajouter plusieurs lignes, chaque ligne ayant : désignation, quantité, prix unitaire HT, taux de TVA.
- Interface en français, champs obligatoires clairement signalés.

Format attendu : un formulaire fonctionnel, accessible depuis le bouton "Nouveau devis" et le bouton "Nouvelle facture", avec le type pré-sélectionné selon le bouton cliqué.
```

### Prompt 1.3 — Ajout et suppression de lignes

```text
Contexte : Le formulaire de devis/facture existe. Il contient une zone de lignes, mais une seule ligne est affichée.

Objectif : Permettre d'ajouter et de supprimer des lignes dynamiquement, sans recharger la page.

Contraintes :
- Le bouton "Ajouter une ligne" ajoute une nouvelle ligne vide en bas de la liste.
- Chaque ligne possède un bouton de suppression.
- La première ligne ne peut pas être supprimée (il doit toujours en rester au moins une).

Format attendu : un formulaire dans lequel on peut saisir autant de lignes que nécessaire, en ajouter et en supprimer, le tout sans recharger la page.
```

### Prompt 1.4 — Valeurs d'exemple

```text
Contexte : Le formulaire est fonctionnel mais vide au premier affichage, ce qui ne montre pas à quoi ressemble un document complet.

Objectif : Pré-remplir le formulaire avec des valeurs d'exemple au premier affichage.

Contraintes :
- Les valeurs doivent être clairement fictives.
- L'utilisateur doit pouvoir les modifier ou les effacer normalement.
- Ne pas pré-remplir lors d'une modification d'un document existant.

Format attendu : au premier affichage du formulaire, les champs sont pré-remplis avec un client fictif et deux lignes d'exemple.
```

### Points de vigilance

- Vérifiez que le formulaire est lisible et que les champs obligatoires sont clairement indiqués.
- Vérifiez que l'ajout et la suppression de lignes fonctionnent sans recharger la page.
- Vérifiez que le choix devis / facture modifie bien le libellé des dates (validité pour un devis, échéance pour une facture).

**Résultat attendu :** un formulaire fonctionnel dans lequel on peut saisir un document et ses lignes.

---

## Étape 2 : calcul automatique des totaux

**Durée : 30 min**

### Prompt 2.1 — Calcul par ligne

```text
Contexte : Le formulaire de devis/facture permet de saisir des lignes avec désignation, quantité, prix unitaire HT et taux de TVA.

Objectif : Calculer automatiquement, pour chaque ligne, le total HT et le total TTC.

Contraintes :
- Total HT d'une ligne = quantité × prix unitaire HT.
- Total TTC d'une ligne = total HT + TVA de la ligne.
- Les totaux s'affichent à mesure de la saisie, sans bouton "Calculer".

Format attendu : chaque ligne affiche son total HT et son total TTC, mis à jour en temps réel.
```

### Prompt 2.2 — Totaux du document

```text
Contexte : Les totaux par ligne sont calculés. Je veux maintenant les totaux du document complet.

Objectif : Afficher en bas du formulaire le total HT, le total de TVA et le total TTC du document.

Contraintes :
- Les totaux se mettent à jour automatiquement à chaque modification d'une ligne.
- Les totaux sont lisibles et mis en évidence (par exemple dans un encadré en bas du formulaire).

Format attendu : un bloc "Totaux" sous la liste des lignes, avec trois valeurs : Total HT, Total TVA, Total TTC.
```

### Prompt 2.3 — Format des montants

```text
Contexte : Les totaux s'affichent mais sans format monétaire français lisible.

Objectif : Formater tous les montants en euros, avec deux décimales et un espace comme séparateur de milliers.

Contraintes :
- Format attendu : 1 250,00 €
- Ne pas modifier les calculs, seulement l'affichage.

Format attendu : tous les montants de l'application (lignes et totaux) sont affichés au format 1 250,00 €.
```

### Prompt 2.4 — Résistance aux erreurs de saisie

```text
Contexte : Si un champ quantité ou prix est vide ou contient du texte, l'application peut afficher une erreur.

Objectif : Rendre le calcul robuste aux saisies invalides.

Contraintes :
- Un champ vide ou invalide est traité comme 0.
- Aucune erreur JavaScript ne doit apparaître dans la console.
- L'utilisateur ne doit pas être bloqué : il peut corriger sa saisie.

Format attendu : en saisissant un texte ou un champ vide dans une ligne, les totaux affichent 0,00 €, sans message d'erreur technique.
```

### Vérification

1. Saisissez un document de test avec trois lignes et des taux de TVA différents (0 %, 10 %, 20 %).
2. Vérifiez les totaux à la main : la ligne 2 avec 3 × 45,50 € HT et TVA 10 % doit donner 136,50 € HT et 150,15 € TTC.
3. Si le calcul est faux, formulez précisément le problème à l'Agent avec les chiffres attendus et les chiffres obtenus.

**Résultat attendu :** un calcul fiable et lisible, vérifié sur un cas manuel.

---

## Étape 3 : enregistrement et base de données

**Durée : 30 min**

### Prompt 3.1 — Schéma de la base de données

```text
Contexte : L'application permet de saisir un devis ou une facture mais rien n'est encore enregistré.

Objectif : Ajouter une base de données pour conserver les clients et les documents.

Contraintes :
- Table "clients" : id, nom, adresse, email, numero_tva.
- Table "documents" : id, type (devis ou facture), numero, date_emission, date_validite, client_id, statut.
- Table "lignes" : id, document_id, designation, quantite, prix_unitaire_ht, taux_tva.
- Utiliser la base de données intégrée de Replit.

Format attendu : les tables sont créées et visibles dans le panneau Database de Replit.
```

### Prompt 3.2 — Enregistrement et numérotation

```text
Contexte : Les tables existent. Le formulaire de devis/facture est fonctionnel.

Objectif : Enregistrer le document et ses lignes dans la base de données lors de la validation du formulaire, avec une numérotation automatique.

Contraintes :
- Les devis sont numérotés DEV-2025-001, DEV-2025-002, etc.
- Les factures sont numérotées FAC-2025-001, FAC-2025-002, etc.
- Les deux compteurs sont indépendants.
- La numérotation ne doit jamais produire de doublon ni de trou.
- Le statut initial est "brouillon".

Format attendu : à chaque validation du formulaire, un nouveau document est créé en base avec un numéro unique, et ses lignes sont enregistrées.
```

### Prompt 3.3 — Gestion du client

```text
Contexte : Le formulaire demande les informations du client à chaque création de document.

Objectif : Éviter les doublons de clients dans la base de données.

Contraintes :
- Si l'email du client saisi n'existe pas en base, créer une nouvelle fiche client.
- Si l'email existe déjà, réutiliser la fiche existante.
- Mettre à jour le nom et l'adresse si l'utilisateur a saisi des informations différentes.

Format attendu : en créant deux documents pour le même client, une seule fiche client existe en base.
```

### Prompt 3.4 — Confirmation après enregistrement

```text
Contexte : Après la validation du formulaire, l'utilisateur ne sait pas si l'enregistrement a réussi.

Objectif : Rediriger l'utilisateur vers la page de liste et afficher un message de confirmation.

Contraintes :
- Le message doit contenir le numéro du document créé (ex. "Le devis DEV-2025-003 a bien été enregistré").
- Le message doit disparaître après quelques secondes.
- En cas d'erreur, afficher un message d'erreur clair, sans code technique.

Format attendu : après chaque enregistrement, l'utilisateur revient à la liste des documents avec un message de confirmation visible.
```

### Points de vigilance

- Vérifiez qu'après enregistrement, le document apparaît bien dans la base de données.
- Vérifiez que la numérotation ne saute pas de numéro et ne crée pas de doublon.
- Vérifiez qu'un même client n'est pas créé deux fois.

**Résultat attendu :** chaque document créé est enregistré, numéroté et associé à un client.

---

## Étape 4 : liste, recherche et filtres

**Durée : 30 min**

### Prompt 4.1 — Page de liste

```text
Contexte : Les documents sont enregistrés en base mais aucune page ne les affiche.

Objectif : Créer une page "Documents" qui liste tous les devis et factures.

Contraintes :
- Colonnes : numéro, type, client, date, montant TTC, statut.
- Tri par date décroissante par défaut.
- Montants au format 1 250,00 €.

Format attendu : une page accessible depuis le menu, affichant tous les documents enregistrés.
```

### Prompt 4.2 — Recherche et filtres

```text
Contexte : La page de liste affiche tous les documents mais devient vite longue.

Objectif : Ajouter une recherche et des filtres pour retrouver un document rapidement.

Contraintes :
- Recherche par numéro de document ou nom de client.
- Filtres : type (devis / facture), statut (brouillon, envoyé, payé, impayé), période (date de début, date de fin).
- Les filtres doivent se combiner (ex. factures impayées du mois dernier).
- Un bouton "Réinitialiser" remet tous les filtres à zéro.

Format attendu : une barre de recherche, trois filtres et un bouton de réinitialisation au-dessus de la liste.
```

### Prompt 4.3 — Actions sur chaque document

```text
Contexte : La liste affiche les documents mais on ne peut rien faire depuis cette page.

Objectif : Ajouter des actions rapides sur chaque document.

Contraintes :
- Bouton "Ouvrir" : afficher le document en lecture.
- Bouton "Modifier" : ouvrir le formulaire pré-rempli.
- Bouton "Marquer comme payé" (factures) ou "Marquer comme accepté" (devis).
- Bouton "Supprimer" avec demande de confirmation.

Format attendu : chaque ligne de la liste propose ces actions, et le statut se met à jour immédiatement après une action.
```

### Prompt 4.4 — Totaux en bas de page

```text
Contexte : La page de liste affiche les documents, mais pas de synthèse.

Objectif : Afficher un récapitulatif en bas de la liste.

Contraintes :
- Nombre total de documents affichés.
- Montant total facturé (factures uniquement).
- Montant total impayé (factures avec statut "impayé").
- Les totaux s'adaptent aux filtres actifs.

Format attendu : un bandeau en bas de la page avec trois indicateurs, mis à jour à chaque changement de filtre.
```

### Points de vigilance

- Vérifiez que les filtres se combinent correctement (ex. factures impayées du mois dernier).
- Vérifiez que le bouton supprimer demande une confirmation avant d'agir.

**Résultat attendu :** une page de liste claire, avec recherche, filtres et actions rapides.

---

## Étape 5 : export PDF et Excel

**Durée : 30 min**

### Prompt 5.1 — Export PDF

```text
Contexte : Les documents sont consultables dans l'application mais ne peuvent pas être envoyés à un client.

Objectif : Ajouter un bouton "Exporter en PDF" sur chaque document.

Contraintes :
- Le PDF contient : en-tête de l'entreprise (nom, adresse, coordonnées), informations du client, détail des lignes, totaux HT, TVA et TTC, numéro du document.
- Mise en page professionnelle, lisible à l'impression.
- Accents et symbole € correctement affichés.

Format attendu : un bouton "Exporter en PDF" sur chaque document, qui télécharge un fichier PDF prêt à envoyer au client.
```

### Prompt 5.2 — Export Excel

```text
Contexte : En plus du PDF, l'utilisateur veut pouvoir retravailler les données dans un tableur.

Objectif : Ajouter un bouton "Exporter en Excel" sur chaque document.

Contraintes :
- Le fichier Excel contient deux feuilles : "Document" (informations générales et totaux) et "Lignes" (détail des lignes).
- Les montants sont au format numérique, pas en texte.
- Le nom du fichier contient le type et le numéro du document.

Format attendu : un bouton "Exporter en Excel" qui télécharge un fichier .xlsx exploitable dans un tableur.
```

### Prompt 5.3 — Mentions obligatoires

```text
Contexte : Une facture doit contenir certaines mentions légales pour être valable.

Objectif : Ajouter les mentions obligatoires en bas du document (PDF et page de lecture).

Contraintes :
- Date d'émission, date d'échéance.
- Conditions de paiement (ex. "Paiement à 30 jours").
- Pénalités de retard (ex. "En cas de retard de paiement, une pénalité de 3 fois le taux d'intérêt légal sera appliquée").
- Mention "TVA non applicable, art. 293 B du CGI" si le taux de TVA est à 0 %.

Format attendu : un bloc "Mentions légales" en bas de chaque document, visible dans l'application et dans l'export PDF.
```

### Prompt 5.4 — Nom des fichiers exportés

```text
Contexte : Les fichiers exportés s'appellent tous "document.pdf" ou "export.xlsx" et sont difficiles à classer.

Objectif : Nommer les fichiers exportés avec le type et le numéro du document.

Contraintes :
- Format : FAC-2025-001.pdf, DEV-2025-003.xlsx.
- Pas d'espaces ni de caractères spéciaux dans le nom.

Format attendu : chaque export produit un fichier dont le nom contient le type et le numéro du document.
```

### Points de vigilance

- Vérifiez que le PDF s'ouvre correctement et que les totaux correspondent à ceux affichés.
- Vérifiez que le fichier Excel contient bien toutes les lignes et pas seulement la première.
- Vérifiez que les accents et les symboles (€) s'affichent correctement dans le PDF.

**Résultat attendu :** un export PDF et Excel propre, téléchargeable depuis chaque document.

---

## Étape 6 : tests et discussion

**Durée : 20 min**

### À faire

1. Créez un devis avec trois lignes, exportez-le en PDF, puis vérifiez que les totaux correspondent au calcul manuel.
2. Dupliquez le devis, transformez-le en facture, vérifiez que la numérotation suit bien (FAC-2025-001 après le devis DEV-2025-001).
3. Modifiez le taux de TVA d'une ligne et vérifiez que le total TTC se met à jour partout.
4. Créez un document avec un champ vide ou un texte à la place d'un nombre, vérifiez que l'application ne plante pas.
5. Si un calcul ou un export est faux, formulez le problème à l'Agent avec les chiffres attendus et obtenus.

### Tableau de tests à remplir

| Cas testé | Attendu | Obtenu | Verdict |
|---|---|---|---|
| Devis 3 lignes, TVA mixtes | Totaux corrects | | |
| Transformation devis → facture | Numérotation continue | | |
| Modification du taux de TVA | Total TTC mis à jour | | |
| Champ quantité vide | 0,00 €, pas d'erreur | | |
| Export PDF | Totaux conformes | | |
| Export Excel | Toutes les lignes présentes | | |

### Discussion à mener

- **Le gestionnaire vérifie toujours** : quelles mentions légales ou quels calculs doivent impérativement être relus avant d'envoyer un document à un client ?
- **Confidentialité** : seules des données fictives ont été utilisées ici. Que faudrait-il changer avant d'utiliser de vraies données clients ?
- **Traçabilité** : comment retrouver, plus tard, qui (l'IA ou un humain) a créé, modifié ou supprimé un document ?
- **Cohérence** : comment empêcher la suppression d'une facture déjà payée ?

**Résultat attendu :** un tableau de tests avec les cas vérifiés et leur résultat, plus des notes de discussion sur les limites.

---

## Documenter le lab

Rassemblez tout ce qui a été produit dans un dossier de projet clair, puis déployez l'application avec le bouton **Deploy** de Replit.

### Modèle de fiche projet

```markdown
# Lab Facturation — Application web de factures et de devis

## Besoin
[Résumé du scénario et de l'objectif]

## Architecture
[Front-end, back-end, base de données, export PDF/Excel]

## Modèle de données
[Tables clients, documents, lignes]

## Tests réalisés
[Calcul des totaux, numérotation, export, transformation devis → facture]

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
git add LAB2_FACTURATION.md
git commit -m "Lab 2 Facturation : application web de factures et de devis"
git push
```

Si c'est le premier fichier du dépôt :

```bash
git init
git add LAB2_FACTURATION.md
git commit -m "Lab 2 Facturation : application web de factures et de devis"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

---

## Aller plus loin

- Module 6 du programme : *Tester et déboguer une application IA* — utile si l'Agent produit une erreur pendant la construction.
- Module 7 : *Sécurité, gouvernance et déploiement* — pour approfondir la protection des données clients et la traçabilité des documents.
- Idées d'extension : envoi du PDF par email, facture récurrente pour les abonnements, relances automatiques pour les impayés, tableau de bord du chiffre d'affaires.
