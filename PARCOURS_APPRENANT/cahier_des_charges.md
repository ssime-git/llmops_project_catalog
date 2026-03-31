# Projet fil rouge — Orientation & Parcours Apprenant

## Contexte

SkillPath Academy accompagne des professionnels tech dans leur montée en compétences. Les conseillers pédagogiques passent 2h par entretien à analyser manuellement le profil d'un apprenant, croiser avec le catalogue et construire un parcours adapté.

## Données disponibles

- Catalogue de formations (contenu, prérequis, compétences acquises, durée, format)
- Fiches métiers cibles (compétences requises, niveaux, certifications valorisées)
- Profils apprenants (compétences actuelles, expérience, objectif, disponibilité)
- Historique des évaluations passées (scores, formations suivies)
- Catalogue des certifications (prérequis, validité, reconnaissance marché)
- Contenu pédagogique des formations (objectifs, programme, niveau)

## Capacités attendues du système

Le système doit aider les conseillers à construire des parcours personnalisés.
Capacités utiles envisageables (non exhaustif) :

- Recommander un parcours adapté au profil et à l'objectif d'un apprenant
- Identifier les lacunes d'un profil par rapport à un objectif cible
- Évaluer si un apprenant est prêt pour une certification donnée
- Estimer la durée et la charge d'un parcours

## Contraintes techniques

- Stack 100% open source (voir [README.md](/Users/seb/Documents/projets_llmops_opensource/README.md))
- Déployable via Docker Compose
- Suivi d'expérimentation obligatoire (MLflow)
- Pipeline d'évaluation automatisé sur eval_recommendations.csv
- Durée : 3 semaines

## Ce que vous devez décider (Phase 1 — Cadrage)

- Quel est votre cas d'usage MVP principal ?
- Quelles données vectorisez-vous ? Lesquelles gardez-vous en SQL ?
- Comment scorez-vous explicitement un parcours (pas juste similarité) ?
- Comment évaluez-vous la qualité d'une recommandation ?
