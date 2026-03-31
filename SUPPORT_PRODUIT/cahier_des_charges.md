# Projet fil rouge — Support Produit Intelligent

## Contexte

Nexus Platform est une solution SaaS B2B de gestion de projets techniques. L'équipe support traite en moyenne 200 tickets/mois. Les agents passent 40% de leur temps à chercher la bonne documentation et à identifier si le problème est connu.

## Données disponibles

- Documentation produit (guides d'installation v2 et v3, FAQ, référence API, release notes)
- Historique de tickets (catégorie, sévérité, client, version, résolution)
- Catalogue clients (version utilisée, tier SLA, secteur)
- Matrice SLA (temps de réponse et résolution par tier et sévérité)
- Base de problèmes connus (symptôme, contournement, version corrigée)

## Capacités attendues du système

Le système doit aider les agents support à traiter les incidents plus efficacement.
Sans imposer d'approche, les capacités utiles incluent (liste non exhaustive) :

- Identifier si un problème est connu et proposer un contournement documenté
- Contextualiser un incident selon la version et le profil client
- Structurer une réponse exploitable pour l'agent ou le client
- Évaluer la qualité des réponses produites

## Contraintes techniques

- Stack 100% open source (voir [README.md](../README.md))
- Déployable via Docker Compose
- Suivi d'expérimentation obligatoire (MLflow)
- Pipeline d'évaluation automatisé sur eval_tickets.csv
- Durée : 3 semaines

## Ce que vous devez décider (Phase 1 — Cadrage)

- Quel est votre cas d'usage MVP principal ?
- Quelles données vectorisez-vous ? Lesquelles gardez-vous en SQL ?
- Comment mesurez-vous la qualité de votre système ?
- Quel modèle LLM choisissez-vous et pourquoi ?
