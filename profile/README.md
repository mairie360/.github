<div align="center">

# mairie360

**La suite numérique souveraine des petites communes françaises.**

[Site web](https://mairie360.fr) · [Cahier des charges](https://github.com/mairie360/.github/blob/main/CAHIER_DES_CHARGES.md) · [Contribuer](#contribuer)

</div>

---

Les petites mairies travaillent souvent avec des outils qui ne communiquent pas entre eux, vieillissants, et dont la sécurité laisse à désirer.
**mairie360** les remplace par une seule plateforme : les agents y gèrent leurs projets, leurs agendas, leurs échanges et leurs formations, dans un environnement hébergé en France et dédié à leur commune.

> **Statut :** MVP fonctionnel, en test pilote auprès de deux communes partenaires de La Réunion (Saint-Paul et Saint-André).

## Nos principes

- **Souveraineté :** chaque mairie dispose de sa propre instance sur un serveur dédié. Il n'y a pas de multi-tenant et aucune donnée n'est partagée entre communes.
- **Un socle commun :** toutes les communes partagent le même produit standardisé et maintenu, sans développements sur mesure à maintenir pour chacune.
- **Stabilité avant tout :** nous faisons évoluer les fonctionnalités dans la durée plutôt que de courir après la dernière technologie à la mode.
- **L'IA reste facultative :** elle est intégrée progressivement, toujours signalée comme telle, et l'outil s'utilise entièrement sans elle.
- **Un accompagnement, pas seulement un logiciel :** chaque déploiement s'accompagne de formation et de support.

## Modules

| Module | Ce qu'il fait | Front | BFF | API |
|---|---|---|---|---|
| **Connexion** | Authentification des agents | [Login_Web_Service](https://github.com/mairie360/Login_Web_Service) | [BFF_user](https://github.com/mairie360/BFF_user) | [Core_API](https://github.com/mairie360/Core_API) |
| **Tableau de bord** | Vue d'ensemble de l'activité de la mairie | [Dashboard_Web_Service](https://github.com/mairie360/Dashboard_Web_Service) | [BFF_Dashboard](https://github.com/mairie360/BFF_Dashboard) | [Core_API](https://github.com/mairie360/Core_API) |
| **Projets** | Planifier, suivre et mener les actions municipales | [Projects_Web_Service](https://github.com/mairie360/Projects_Web_Service) | [BFF_Project](https://github.com/mairie360/BFF_Project) | [Project_API](https://github.com/mairie360/Project_API) |
| **Calendrier** | Événements, réunions et plannings partagés | [Calendars_Web_Service](https://github.com/mairie360/Calendars_Web_Service) | [BFF_Calendar](https://github.com/mairie360/BFF_Calendar) | [Calendar_API](https://github.com/mairie360/Calendar_API) |
| **Messagerie** | Communication interne entre agents et services | [Messages_Web_Service](https://github.com/mairie360/Messages_Web_Service) | [BFF_Message](https://github.com/mairie360/BFF_Message) | [Message_API](https://github.com/mairie360/Message_API) |
| **E-learning** | Parcours de formation : vidéos, documents, quiz | [Elearning_Web_Service](https://github.com/mairie360/Elearning_Web_Service) | [BFF_Elearning](https://github.com/mairie360/BFF_Elearning) | [ELearning_API](https://github.com/mairie360/ELearning_API) |
| **Paramètres** | Préférences du compte et de la commune | [Settings_Web_Service](https://github.com/mairie360/Settings_Web_Service) | [BFF_Settings](https://github.com/mairie360/BFF_Settings) | [Core_API](https://github.com/mairie360/Core_API) |
| **Administration** | Gestion des agents, des rôles et des droits | [Administrator_Web_Service](https://github.com/mairie360/Administrator_Web_Service) | — | [Core_API](https://github.com/mairie360/Core_API) |

La conformité réglementaire (RGPD notamment) est assurée par [Compliance_API](https://github.com/mairie360/Compliance_API).

## Architecture

```
            Navigateur de l'agent
                     │
   ┌─────────────────▼─────────────────┐
   │  Fronts  — Next.js (SSR, CSP)      │   un front par module
   └─────────────────┬─────────────────┘
   ┌─────────────────▼─────────────────┐
   │  BFFs    — Node.js / TypeScript    │   agrégation, sans base de données
   └─────────────────┬─────────────────┘
   ┌─────────────────▼─────────────────┐
   │  APIs    — Rust                    │   logique métier
   └─────────────────┬─────────────────┘
          PostgreSQL (Liquibase) · Redis
```

Chaque mairie dispose de sa propre instance Kubernetes. Le déploiement suit une approche GitOps avec Argo CD, et l'infrastructure est provisionnée avec Terraform et Ansible.

### Bibliothèques et modèles

| Dépôt | Rôle |
|---|---|
| [API_lib](https://github.com/mairie360/API_lib) · [API_template](https://github.com/mairie360/API_template) | Socle commun et modèle des APIs Rust |
| [bffs_lib](https://github.com/mairie360/bffs_lib) · [Bff_Template_Repo](https://github.com/mairie360/Bff_Template_Repo) | Socle commun et modèle des BFFs |
| [lib-components](https://github.com/mairie360/lib-components) | Composants d'interface partagés entre les fronts |
| [Database](https://github.com/mairie360/Database) | Schéma et migrations Liquibase |

### Infrastructure et outillage

| Dépôt | Rôle |
|---|---|
| [Infra](https://github.com/mairie360/Infra) | Provisionnement des machines (Terraform) |
| [ansible](https://github.com/mairie360/ansible) | Configuration des serveurs |
| [Deploiment](https://github.com/mairie360/Deploiment) | Manifestes Kubernetes et Argo CD |
| [CICD](https://github.com/mairie360/CICD) | Workflows de CI/CD réutilisables |
| [renovate-config](https://github.com/mairie360/renovate-config) | Configuration partagée de Renovate |
| [QA_Agent](https://github.com/mairie360/QA_Agent) | Agent de vérification qualité |
| [mairie360.github.io](https://github.com/mairie360/mairie360.github.io) | Site vitrine [mairie360.fr](https://mairie360.fr) |

## Livraison et versions

- **Une seule branche (`main`) et trois environnements**, chacun sur sa propre machine : `dev` → `staging` → `prod`. Le passage en staging puis en prod se déclenche à la main.
- **Une version globale du produit :** une release `X.Y.Z` fige la combinaison exacte des versions de tous les services. Les mairies montent de version d'un bloc, sans gérer elles-mêmes la compatibilité entre services.
- **Ordre de déploiement :** migration de la base → APIs → BFFs → fronts, avec une sauvegarde de la base avant chaque montée de version.
- **Images Docker** publiées sur GitHub Packages.

## Qualité et sécurité

La qualité repose sur la CI : chaque changement passe des tests unitaires, d'intégration, end-to-end, de performance, de sécurité et d'accessibilité avant d'être intégré.

`semgrep` · `cargo audit` · `npm audit` · `OWASP ZAP` · `k6` · `Newman` · `Renovate`

## Contribuer

- [Gestion des versions](https://github.com/mairie360/.github/blob/main/GESTION_DES_VERSIONS.md) : versionnage et conventions de commits
- [Tests et qualité](https://github.com/mairie360/.github/blob/main/TESTS_ET_QUALITE.md) : stratégie de tests et CI
- [Gestion des fonctionnalités](https://github.com/mairie360/.github/blob/main/GESTION_DES_FONCTIONNALITES.md) : de la conception au déploiement
- [Revue de code](https://github.com/mairie360/.github/blob/main/REVUE_DE_CODE.md) : bonnes pratiques de relecture
- [Collaboration](https://github.com/mairie360/.github/blob/main/COLLABORATION.md) : organisation du travail en équipe
- [Cahier des charges](https://github.com/mairie360/.github/blob/main/CAHIER_DES_CHARGES.md) : fonctionnalités recensées

## Contact

Vous êtes une mairie et le projet vous intéresse ? Rendez-vous sur **[mairie360.fr](https://mairie360.fr)**.

<div align="center"><sub>Fait en France, entre la Loire-Atlantique et La Réunion.</sub></div>
