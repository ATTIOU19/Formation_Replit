# Projet final — Application IA métier

> Module 8 du programme *Concevoir, développer, tester, sécuriser et déployer une application métier avec l'IA*.
> Outil : [Replit](https://replit.com) · Durée indicative : 3 h · Seul ou en groupe.

## Objectif du projet

Après les labs RH, Finance et Service client, vous connaissez la méthode. Le projet final consiste à l'appliquer **seul, à un problème de votre choix**, du cadrage jusqu'à la soutenance.

**Vous devez montrer que vous savez** :
- identifier un problème métier réel et le cadrer ;
- construire une application avec au moins une fonctionnalité IA ;
- la tester, la sécuriser, la déployer ;
- expliquer et défendre vos choix, et nommer les limites de ce que vous avez fait.

> Le projet final n'est pas seulement une application qui fonctionne. Vous devez pouvoir expliquer **pourquoi** vous l'avez construite ainsi, **comment** vous l'avez testée, et **quelles sont ses limites**.

---

## Sommaire des étapes

| # | Étape | Durée | Ce que vous produisez |
|---|---|---|---|
| 1 | [Problème métier et cahier des charges](#étape-1--problème-métier-et-cahier-des-charges) | 30 min | Cahier des charges + workflow |
| 2 | [Construction et fonction IA](#étape-2--construction-et-fonction-ia) | 70 min | Application fonctionnelle |
| 3 | [Test, correction, sécurisation](#étape-3--test-correction-sécurisation) | 30 min | Jeux de tests + résultats |
| 4 | [Déploiement et documentation](#étape-4--déploiement-et-documentation) | 20 min | Application déployée + dossier |
| 5 | [Soutenance](#étape-5--soutenance) | 30 min | Présentation de 5 à 10 min |

---

## Étape 1 : problème métier et cahier des charges

**Durée : 30 min**

### À faire

1. **Choisissez un problème métier** que vous connaissez bien : le vôtre, celui d'un proche, ou un cas plausible dans votre secteur. Évitez de reproduire un des trois labs à l'identique — inspirez-vous de la méthode, pas du résultat.
2. **Rédigez 3 à 5 user stories**, au format :
   > En tant que [utilisateur], je veux [action], afin de [bénéfice].
3. **Définissez les critères d'acceptation** : comment saurez-vous que chaque fonction est terminée ?
4. **Notez ce qui est hors périmètre** : ce que l'application ne fera volontairement pas, pour rester réaliste en 3 h de construction.
5. **Dessinez le workflow**, en identifiant où intervient l'IA et où intervient l'humain :

   ```text
   Entrée → Traitement → Analyse par l'IA → Validation humaine → Sortie
   ```

### Questions pour vous aider à choisir un sujet

- Quelle tâche répétitive, dans mon métier ou celui d'un proche, prend du temps mais suit toujours la même logique ?
- Où une décision automatique aurait-elle besoin d'être expliquée et validée par un humain ?
- Quelles données fictives puis-je préparer facilement pour tester ?

**Résultat attendu :** un cahier des charges court (une page suffit), avec les user stories, les critères d'acceptation, le hors périmètre et le schéma du workflow.

---

## Étape 2 : construction et fonction IA

**Durée : 70 min**

### À faire

1. Découpez votre workflow en étapes de prompts, comme dans les labs (une étape = un prompt = un test).
2. Construisez avec l'Agent Replit, dans l'ordre : d'abord la structure (formulaire, import, ou point d'entrée), puis la fonction IA, puis l'affichage des résultats.
3. Intégrez **au moins une fonctionnalité IA** clairement identifiable (analyse, classification, génération de texte, notation, recherche documentaire…).
4. Ajoutez **une étape de validation humaine** avant toute action définitive (envoi, décision, publication), sur le modèle des trois labs.
5. Après chaque prompt, ouvrez le code généré et vérifiez que vous pouvez expliquer, en langage simple, ce qu'il fait.

### Repères tirés des labs précédents

| Si votre projet ressemble à… | Inspirez-vous de… |
|---|---|
| Un tri ou une notation automatique | Lab RH : grille de scoring explicite et justifiée |
| Un traitement de données répétitif | Lab Finance : pipeline nettoyage → classification → anomalies |
| Une réponse automatique à une demande | Lab Service client : recherche avant de répondre (RAG) et validation avant envoi |

**Résultat attendu :** une application fonctionnelle, avec sa fonction IA et son étape de validation humaine.

---

## Étape 3 : test, correction, sécurisation

**Durée : 30 min**

### À faire

1. **Construisez un jeu de tests** avec au moins 5 cas : entrée testée → résultat attendu → résultat obtenu → verdict. Incluez au moins un cas normal, un cas piégé, et un cas limite ou absurde.
2. **Corrigez** les erreurs trouvées avec l'Agent, une par une, en revérifiant après chaque correction qu'elle n'a rien cassé d'autre.
3. **Sécurisez** :
   - toute clé ou mot de passe est dans les **Secrets** de Replit, jamais dans le code ni le chat ;
   - si l'application manipule des données personnelles ou sensibles, vérifiez qu'aucune vraie donnée n'est utilisée en test ;
   - si pertinent, ajoutez un contrôle d'accès simple (qui peut voir ou valider quoi).

**Résultat attendu :** un tableau de tests rempli et une application dont vous avez vérifié la sécurité de base.

---

## Étape 4 : déploiement et documentation

**Durée : 20 min**

### À faire

1. Publiez l'application avec le bouton **Deploy** de Replit.
2. Rédigez le dossier final du projet (modèle ci-dessous).
3. Poussez le dossier sur GitHub à côté de vos labs.

### Modèle de dossier de projet

```markdown
# Projet final — [Nom de votre application]

## Problème métier
[Le besoin identifié, et pour qui]

## Cahier des charges
[User stories, critères d'acceptation, hors périmètre]

## Architecture (workflow)
[Entrée → traitement → IA → validation → sortie, avec le détail de chaque étape]

## Fonctionnalité IA
[Ce que fait l'IA précisément, et comment sa sortie est validée par un humain]

## Tests réalisés
[Votre tableau de tests de l'étape 3]

## Sécurité
[Secrets, données utilisées, contrôle d'accès]

## Limites identifiées
[Ce que l'application ne fait pas, ou ne fait pas bien]

## Justification des choix
[Pourquoi cette architecture plutôt qu'une autre]

## Lien vers l'application déployée
[URL Replit]
```

**Résultat attendu :** l'application est en ligne, et le dossier explique le projet de bout en bout.

---

## Étape 5 : soutenance

**Durée : 30 min (5 à 10 min par projet)**

### Ce qu'il faut couvrir en 5 à 10 minutes

1. **Le problème** : en une phrase, quel besoin résout votre application ?
2. **La démonstration** : montrez l'application en fonctionnement, du début à la fin.
3. **La fonction IA et sa validation** : montrez précisément où l'IA agit et comment un humain garde le contrôle.
4. **Un test qui a échoué puis a été corrigé** : montrez que vous avez su déboguer, pas seulement construire.
5. **Les limites** : nommez au moins une limite réelle de votre application, sans minimiser.

### Grille d'évaluation

| Critère | Ce qui est attendu | Pondération |
|---|---|---:|
| Cadrage du besoin | Problème métier clair, cahier des charges, user stories, workflow | 15 % |
| Application et fonction IA | Application déployée qui fonctionne, fonction IA pertinente | 25 % |
| Tests et débogage | Jeux de tests, résultats, corrections, cas limites couverts | 20 % |
| Sécurité et gouvernance | Secrets, accès, données, validation humaine | 20 % |
| Documentation et limites | Architecture, justification des choix, limites identifiées | 10 % |
| Soutenance | Clarté, capacité à expliquer et défendre les choix | 10 % |

*Pondérations proposées, à ajuster selon le public.*

**Résultat attendu :** une soutenance qui montre non seulement que l'application fonctionne, mais que vous comprenez et assumez ce que vous avez construit.

---

## Pousser ce projet sur GitHub

```bash
git add PROJET_FINAL.md
git commit -m "Projet final : [nom de votre application]"
git push
```

Si c'est le premier fichier du dépôt :

```bash
git init
git add PROJET_FINAL.md
git commit -m "Projet final : [nom de votre application]"
git branch -M main
git remote add origin <URL_DE_VOTRE_DEPOT>
git push -u origin main
```

---

## Rappel des trois questions à ne jamais négliger

- **Pourquoi** ai-je construit l'application ainsi ?
- **Comment** l'ai-je testée ?
- **Quelles** sont ses limites ?

Si vous pouvez répondre clairement aux trois, le projet final est réussi — indépendamment du niveau de sophistication de l'application elle-même.
