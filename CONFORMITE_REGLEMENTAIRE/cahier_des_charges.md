# Projet fil rouge — Conformité Réglementaire Intelligente

## Contexte

Le cabinet AuditPro accompagne des entités soumises aux règlements de l'ACSI.
Les auditeurs passent 60% de leur temps à croiser manuellement des documents
internes avec les textes réglementaires pour identifier des écarts.

## Données disponibles

- Textes réglementaires complets (RGD-2024 sur la gouvernance des données,
  DSI-2023 sur la sécurité des SI, guide d'interprétation officiel,
  décisions de référence passées)
- Registre des entités (secteur, taille, périmètre)
- Registre des contrôles planifiés et réalisés
- Base de non-conformités identifiées
- Registre des risques par entité
- Règlements applicables par type d'entité

## Capacités attendues du système

Le système doit aider les auditeurs à traiter les dossiers de conformité
plus efficacement. Capacités utiles envisageables (non exhaustif) :

- Analyser un document soumis et identifier des écarts réglementaires
- Planifier et prioriser les contrôles à réaliser
- Générer des rapports de conformité structurés
- Contextualiser une question réglementaire par rapport aux textes applicables

## Contraintes techniques

- Stack 100% open source (voir [README.md](/Users/seb/Documents/projets_llmops_opensource/README.md))
- Déployable via Docker Compose
- Suivi d'expérimentation obligatoire (MLflow)
- Pipeline d'évaluation automatisé sur eval_cases.csv
- Durée : 3 semaines

## Ce que vous devez décider (Phase 1 — Cadrage)

- Quel est votre cas d'usage MVP principal ?
- Quelles données vectorisez-vous ? Lesquelles gardez-vous en SQL ?
- Comment gérez-vous la validité temporelle des règlements ?
- Quel modèle LLM choisissez-vous et pourquoi ?
