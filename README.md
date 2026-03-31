# Projets LLMOps Open Source

Ce dépôt rassemble trois sujets de projets fil rouge autour d'un même cadre technique LLMOps, déclinés sur des contextes métier différents. Chaque sujet fournit un jeu de données mixte, un cahier des charges et un socle de déploiement minimal en open source.

L'objectif n'est pas d'imposer un unique MVP, mais de fournir un terrain de cadrage, de conception et d'implémentation pour un système RAG ou agentique industrialisable.

## Contenu du dépôt

Le dépôt contient trois projets indépendants :

- `SUPPORT_PRODUIT` : assistance à la résolution d'incidents support sur un produit SaaS.
- `CONFORMITE_REGLEMENTAIRE` : aide à l'analyse réglementaire et au suivi de conformité.
- `PARCOURS_APPRENANT` : recommandation de parcours de formation et d'orientation.

Chaque dossier inclut :

- `cahier_des_charges.md` : contexte métier, données disponibles, capacités attendues et questions de cadrage.
- `dataset/documents/` : corpus documentaire à exploiter dans une brique de recherche sémantique.
- `dataset/tables/` : données tabulaires à conserver ou exposer via une couche SQL.
- `docker-compose.yml` : base de services pour exécuter une stack locale.
- `GUIDE_SOUTENANCE.md` : éléments de maintien en condition opérationnelle et de maintenance.

## Structure

```text
.
├── SUPPORT_PRODUIT/
├── CONFORMITE_REGLEMENTAIRE/
├── PARCOURS_APPRENANT/
└── README.md
```

## Finalité pédagogique et technique

Chaque projet est conçu pour faire travailler les mêmes décisions structurantes :

- choisir un cas d'usage MVP crédible à partir d'un besoin métier non entièrement figé ;
- répartir les données entre recherche vectorielle, stockage relationnel et éventuel stockage objet ;
- sélectionner un modèle open source pertinent pour la génération ;
- mettre en place une chaîne d'évaluation reproductible ;
- instrumenter le système pour en mesurer la qualité, la latence et l'exploitabilité.

Le dépôt est volontairement orienté vers une logique LLMOps :

- expérimentation traçable ;
- prompts versionnés ;
- évaluation sur jeu de test figé ;
- supervision minimale ;
- déploiement local reproductible.

## Les trois projets

### 1. Support Produit

Contexte :
une équipe support doit traiter des tickets plus vite en s'appuyant à la fois sur de la documentation produit, un historique de tickets, une base d'incidents connus et des informations clients.

Exemples de capacités à construire :

- identifier un problème connu et proposer un contournement documenté ;
- contextualiser une réponse selon la version du client et son niveau de SLA ;
- assister la rédaction d'une réponse exploitable par un agent support.

Références utiles :

- [SUPPORT_PRODUIT/cahier_des_charges.md](SUPPORT_PRODUIT/cahier_des_charges.md)
- [SUPPORT_PRODUIT/GUIDE_SOUTENANCE.md](SUPPORT_PRODUIT/GUIDE_SOUTENANCE.md)

### 2. Conformité Réglementaire

Contexte :
des auditeurs doivent croiser des textes réglementaires, des contrôles, des risques et des non-conformités pour produire une analyse plus rapide et plus cohérente.

Exemples de capacités à construire :

- retrouver les textes applicables à une entité ou à une situation donnée ;
- détecter des écarts entre une situation observée et un cadre réglementaire ;
- structurer un rapport ou une synthèse de conformité.

Références utiles :

- [CONFORMITE_REGLEMENTAIRE/cahier_des_charges.md](CONFORMITE_REGLEMENTAIRE/cahier_des_charges.md)
- [CONFORMITE_REGLEMENTAIRE/GUIDE_SOUTENANCE.md](CONFORMITE_REGLEMENTAIRE/GUIDE_SOUTENANCE.md)

### 3. Parcours Apprenant

Contexte :
des conseillers pédagogiques doivent analyser des profils, des prérequis, des objectifs métiers, des certifications et un catalogue de formations pour bâtir des parcours cohérents.

Exemples de capacités à construire :

- recommander un parcours adapté à un profil et à un objectif cible ;
- identifier les écarts de compétences à combler ;
- estimer l'effort ou la durée d'un parcours ;
- évaluer l'éligibilité à une certification.

Références utiles :

- [PARCOURS_APPRENANT/cahier_des_charges.md](PARCOURS_APPRENANT/cahier_des_charges.md)
- [PARCOURS_APPRENANT/GUIDE_SOUTENANCE.md](PARCOURS_APPRENANT/GUIDE_SOUTENANCE.md)

## Cadre technique commun

Le dépôt suppose une stack 100 % open source. Une combinaison typique est la suivante :

| Besoin | Option open source |
|---|---|
| LLM d'inférence | Ollama avec Mistral, Llama ou modèle compatible |
| Embeddings | `sentence-transformers` |
| Base vectorielle | Qdrant |
| Base relationnelle | PostgreSQL |
| Stockage objet | MinIO |
| API backend | FastAPI |
| Interface simple | Streamlit |
| Tracking d'expériences | MLflow |
| Évaluation RAG | Ragas |
| Monitoring | Prometheus + Grafana |

Cette stack est indicative. L'essentiel est de rester cohérent, déployable localement et justifiable au regard du cas d'usage choisi.

## Principes de cadrage

Le point central de ces sujets est le cadrage. Les données sont suffisamment riches pour permettre plusieurs solutions plausibles.

Les décisions attendues en début de projet sont en général :

- le cas d'usage MVP principal ;
- la stratégie de découpage des données entre vectoriel et SQL ;
- les critères de succès métier et technique ;
- le choix du ou des modèles ;
- la stratégie d'évaluation ;
- les limites connues du système.

Un bon cadrage évite deux erreurs classiques :

- vectoriser tout sans discernement ;
- réduire l'évaluation à un ressenti qualitatif sans protocole stable.

## Exigences LLMOps minimales

Quel que soit le sujet retenu, une implémentation sérieuse doit au minimum couvrir :

### Tracking d'expériences

- journalisation des paramètres de run ;
- suivi des métriques de qualité et de performance ;
- conservation des prompts, sorties et artefacts utiles.

Exemple de paramètres et métriques à suivre :

- modèle ;
- température ;
- chunk size ;
- embedding model ;
- latence ;
- score de faithfulness ;
- coût estimé ou volume de tokens.

### Versionnement des prompts

Les prompts doivent être identifiables, comparables et promouvables. L'objectif n'est pas seulement de stocker un texte, mais de relier chaque version à un protocole d'évaluation stable.

### Évaluation automatisée

Chaque projet fournit un jeu d'évaluation tabulaire :

- `SUPPORT_PRODUIT/dataset/tables/eval_tickets.csv`
- `CONFORMITE_REGLEMENTAIRE/dataset/tables/eval_cases.csv`
- `PARCOURS_APPRENANT/dataset/tables/eval_recommendations.csv`

Une évaluation type peut inclure :

- `faithfulness` ;
- `answer_relevancy` ;
- `context_precision` ;
- métriques métier spécifiques au sujet.

### Monitoring

Le système doit permettre de suivre au minimum :

- disponibilité des services ;
- temps de réponse ;
- erreurs applicatives ;
- évolution des scores de qualité ou signaux de dérive.

## Architecture de référence

L'architecture cible peut rester simple :

1. ingestion de documents et de tables ;
2. préparation des chunks et calcul des embeddings ;
3. alimentation d'une base vectorielle et d'une base SQL ;
4. exposition d'une API de requêtage ;
5. orchestration RAG ou hybride RAG + SQL ;
6. journalisation des runs et évaluation continue.

Une séparation nette entre données documentaires et données structurées est généralement préférable. Elle rend le système plus explicable, plus testable et plus facile à maintenir.

## Démarrage rapide

Chaque projet dispose de son propre `docker-compose.yml`. Le point de départ le plus simple consiste à se placer dans le dossier concerné puis à démarrer les services.

```bash
cd SUPPORT_PRODUIT
docker compose up -d
```

Même principe pour :

```bash
cd CONFORMITE_REGLEMENTAIRE
docker compose up -d
```

ou :

```bash
cd PARCOURS_APPRENANT
docker compose up -d
```

Avant d'aller plus loin, vérifiez dans chaque dossier :

- les services réellement exposés par le `docker-compose.yml` ;
- les dépendances applicatives non incluses dans ce dépôt ;
- les variables d'environnement nécessaires ;
- le périmètre exact du MVP que vous souhaitez démontrer.

## Méthode de travail recommandée

Une progression réaliste est la suivante :

1. lire le cahier des charges du projet choisi ;
2. inspecter les documents et tables disponibles ;
3. définir le MVP et les critères d'évaluation ;
4. concevoir la stratégie de retrieval et d'accès SQL ;
5. implémenter un premier pipeline de bout en bout ;
6. instrumenter les runs avec MLflow ;
7. lancer une première campagne d'évaluation ;
8. itérer sur les prompts, le chunking et les règles d'orchestration ;
9. documenter les limites et la soutenabilité.

## Ce que ce dépôt fournit, et ce qu'il ne fournit pas

Le dépôt fournit :

- des contextes métier crédibles ;
- des jeux de données mixtes ;
- une base de cadrage ;
- une structure de projet simple à prendre en main.

Le dépôt ne fournit pas :

- une implémentation applicative complète ;
- un schéma d'architecture imposé ;
- un unique cas d'usage officiel ;
- un protocole d'évaluation exhaustif déjà prêt à l'emploi.

## Références internes

- [SUPPORT_PRODUIT/cahier_des_charges.md](SUPPORT_PRODUIT/cahier_des_charges.md)
- [CONFORMITE_REGLEMENTAIRE/cahier_des_charges.md](CONFORMITE_REGLEMENTAIRE/cahier_des_charges.md)
- [PARCOURS_APPRENANT/cahier_des_charges.md](PARCOURS_APPRENANT/cahier_des_charges.md)
