# Cahier des Charges - Mairie360

**Application de Gestion Municipale**

Version: 1.0
Date: Octobre 2024

---

## 📋 Table des Matières

1. [Vue d'ensemble du projet](#1-vue-densemble-du-projet)
2. [Architecture globale](#2-architecture-globale)
3. [Spécifications techniques générales](#3-spécifications-techniques-générales)
4. [Module Tableau de Bord](#4-module-tableau-de-bord)
5. [Module Projets](#5-module-projets)
6. [Module Messagerie](#6-module-messagerie)
7. [Module E-mails](#7-module-e-mails)
8. [Module Fichiers](#8-module-fichiers)
9. [Module Formation](#9-module-formation)
10. [Module Calendrier](#10-module-calendrier)
11. [Module Paramètres](#11-module-paramètres)
12. [Layout et Navigation](#12-layout-et-navigation)
13. [Exigences techniques](#13-exigences-techniques)

---

## 1. Vue d'ensemble du projet

### 1.1 Objectif
Mairie360 est une plateforme complète de gestion municipale permettant aux employés de la mairie de gérer efficacement leurs projets, communications, documents, formations et événements dans une interface unifiée et responsive.

### 1.2 Public cible
- Employés municipaux
- Direction générale
- Différents services (Finances, Urbanisme, Culture, RH, etc.)

### 1.3 Périmètre fonctionnel
L'application comprend 8 modules principaux :
- Dashboard (Tableau de bord)
- Projets
- Messagerie interne
- E-mails
- Gestion de fichiers
- Centre de formation (E-learning)
- Calendrier & Événements
- Paramètres

---

## 2. Architecture globale

### 2.1 Stack technique
- **Frontend**: Next
- **Styling**: Tailwind CSS
- **Components UI**: Lib-Components
- **State Management**: React Hooks (useState, useEffect)

### 2.2 Responsive Design
- **Mobile first**: Optimisation pour toutes les tailles d'écran
- **Breakpoints**:
  - Mobile: < 640px
  - Tablet: 640px - 1024px
  - Desktop: > 1024px
- **Adaptabilité**: Layouts flexibles avec CSS Grid et Flexbox

---

## 3. Spécifications techniques générales

### 3.1 Typographie
- Utilisation de la typographie par défaut définie dans `globals.css`
- Pas de classes Tailwind pour les tailles de police sauf modification explicite
- Hiérarchie claire des titres (h1, h2, h3, etc.)

### 3.2 Couleurs et thèmes
- Système de design tokens définis dans `globals.css`
- Support du mode clair/sombre (via paramètres)
- Couleurs sémantiques pour les statuts et priorités

### 3.3 Composants réutilisables
Utilisation systématique des composants implémenter dans la lib-components

---

## 4. Module Tableau de Bord

### 4.1 Description
Page d'accueil affichant une vue d'ensemble des activités et statistiques importantes.

### 4.2 Fonctionnalités

#### 4.2.1 Statistiques principales
**Cartes de statistiques (4 métriques)**
- **Projets actifs**: Nombre total avec évolution mensuelle (+/-)
- **Citoyens servis**: Compteur avec pourcentage d'évolution
- **Documents traités**: Total mensuel avec tendance
- **Événements du mois**: Nombre d'événements planifiés

**Affichage**:
- Grid responsive (2 colonnes mobile, 4 colonnes desktop)
- Icônes colorées pour chaque métrique
- Indicateur de tendance (positif/négatif)
- Badges colorés selon le type de donnée

#### 4.2.2 Projets récents
**Liste des projets en cours**
- Nom du projet
- Statut (En cours, Terminé)
- Barre de progression (0-100%)
- Date d'échéance
- Bouton "Voir tous" pour accès rapide

**Données affichées**:
- Maximum 3 projets
- Tri par date de modification
- Progress bar visuelle

#### 4.2.3 Tâches en attente
**Liste des tâches prioritaires**
- Titre de la tâche
- Priorité (Haute, Moyenne, Basse)
- Échéance (Aujourd'hui, Demain, X jours)
- Badge coloré selon la priorité:
  - Haute: Rouge
  - Moyenne: Orange
  - Basse: Vert

**Affichage**:
- Maximum 3 tâches
- Indicateur visuel (point coloré)
- Bouton "Voir toutes"

#### 4.2.4 Actions rapides
**Raccourcis vers fonctionnalités principales**
- Nouveau document
- Planifier événement
- Contacter équipe
- Voir rapports

**Présentation**:
- Grid 2x2
- Icônes + Labels
- Boutons interactifs

#### 4.2.5 Événements à venir
**Liste chronologique des prochains événements**
- Titre de l'événement
- Date et heure
- Lieu
- Card colorée avec date en évidence

**Données**:
- Maximum 3 événements
- Tri chronologique
- Lien vers le calendrier complet

#### 4.2.6 Aperçu des performances
**Indicateurs de performance globaux**
- Projets terminés ce trimestre
- Délai moyen de traitement
- Alertes actives nécessitant attention

**Visualisation**:
- 3 cartes avec icônes
- Chiffres clés mis en évidence
- Descriptions contextuelles

### 4.3 Responsive
- **Mobile**: Stack vertical, cartes stats 2 colonnes
- **Tablet**: Grid mixte, optimisation de l'espace
- **Desktop**: Layout complet sur 2 colonnes principales

---

## 5. Module Projets

### 5.1 Description
Module de gestion de projets municipaux avec système Kanban, vue grille et vue table inspiré de GitHub Projects.

### 5.2 Fonctionnalités

#### 5.2.1 Vues multiples
**3 modes d'affichage**:

**Vue Kanban (défaut)**
- Colonnes par statut:
  - À faire
  - En cours
  - En révision
  - Terminé
- Drag & drop entre colonnes
- Cartes compactes avec informations essentielles
- Compteur de projets par colonne
- Bouton d'ajout rapide par colonne

**Vue Grille**
- Disposition en cartes (3 colonnes desktop)
- Cartes détaillées avec toutes les informations
- Hover effects
- Layout responsive (1-3 colonnes selon écran)

**Vue Table**
- Tableau complet avec colonnes:
  - Projet (nom + description)
  - Statut
  - Responsable (avatar + nom)
  - Priorité
  - Progression (barre + %)
  - Échéance
  - Actions (menu dropdown)
- Tri et filtrage
- Actions en masse possibles

#### 5.2.2 Système de filtrage avancé
**Barre de filtres**:
- Recherche textuelle (titre et description)
- Filtre par statut (tous, à faire, en cours, révision, terminé)
- Filtre par priorité (tous, haute, moyenne, basse)
- Filtrage en temps réel

#### 5.2.3 Détails des projets
**Informations affichées sur chaque carte**:
- Titre et description
- Statut avec icône et couleur
- Responsable et équipe (avatars)
- Barre de progression (%)
- Étiquettes/labels (max 2 visibles + compteur)
- Nombre de tâches (complétées/total)
- Priorité avec indicateur coloré
- Date d'échéance avec indicateurs:
  - Rouge si dépassée
  - Orange si < 7 jours
  - Gris sinon
- Menu d'actions (Modifier, Dupliquer, Supprimer)

#### 5.2.4 Gestion des statuts
**4 statuts définis**:
- **À faire**: Gris, icône AlertCircle
- **En cours**: Bleu, icône Clock
- **En révision**: Orange, icône Eye
- **Terminé**: Vert, icône CheckCircle

#### 5.2.5 Gestion des priorités
**3 niveaux**:
- **Haute**: Rouge
- **Moyenne**: Orange
- **Basse**: Vert

#### 5.2.6 Drag & Drop (Kanban)
- Déplacement fluide des cartes
- Animation pendant le drag
- Visual feedback (zone de drop highlight)
- Mise à jour instantanée du statut
- Effet d'opacité et rotation lors du drag

#### 5.2.7 Actions sur les projets
- Créer un nouveau projet
- Modifier un projet existant
- Dupliquer un projet
- Supprimer un projet
- Changer le statut (drag & drop ou menu)
- Voir les détails complets

### 5.3 Responsive
- **Mobile**: Vue Kanban en scroll horizontal, cartes optimisées
- **Tablet**: Transition progressive vers layout desktop
- **Desktop**: Toutes les vues pleinement fonctionnelles

---

## 6. Module Messagerie

### 6.1 Description
Système de messagerie interne en temps réel entre employés municipaux.

### 6.2 Fonctionnalités

#### 6.2.1 Interface principale
**Layout 2 colonnes (3 sur desktop)**:
- Sidebar des contacts (gauche)
- Zone de conversation (droite)
- Responsive: Mobile = onglets alternatifs

#### 6.2.2 Liste des contacts
**Sidebar gauche**:
- Barre de recherche de contacts
- Liste scrollable des conversations
- Pour chaque contact:
  - Avatar avec initiales
  - Nom complet
  - Service/département
  - Dernier message (preview)
  - Timestamp
  - Badge compteur non-lus
  - Indicateur en ligne/hors ligne (point vert/gris)
- Tri par activité récente
- Highlight de la conversation sélectionnée

#### 6.2.3 Création de messages
**Dialog "Nouveau message"**:
- Champ destinataire (select avec liste contacts)
- Zone de texte pour le message
- Boutons Annuler/Envoyer
- Accessible via bouton en haut de liste

#### 6.2.4 Création de groupes
**Dialog "Créer un groupe"**:
- Champ nom du groupe (requis)
- Description (optionnel)
- Sélection multiple de membres (checkboxes)
- Liste scrollable de tous les contacts
- Affichage service pour chaque membre
- Boutons Annuler/Créer
- Validation (minimum 1 membre)

#### 6.2.5 Zone de conversation
**Header de conversation**:
- Bouton retour (mobile)
- Avatar du contact
- Nom et service
- Statut en ligne/hors ligne
- Actions:
  - Appel téléphonique (icône)
  - Appel vidéo (icône)
  - Menu d'options (icône)

**Messages**:
- Bulles de messages:
  - Messages envoyés: Alignés à droite, fond primaire
  - Messages reçus: Alignés à gauche, fond gris
- Nom de l'expéditeur
- Contenu du message
- Timestamp
- Zone scrollable

**Saisie de message**:
- Textarea multi-lignes
- Redimensionnement automatique
- Support Entrée pour envoyer, Shift+Entrée pour nouvelle ligne
- Boutons d'actions:
  - Joindre fichier (icône trombone)
  - Émojis (icône smiley)
  - Envoyer (désactivé si vide)

#### 6.2.6 Fonctionnalités avancées
- Messages épinglés (fonctionnalité prévue)
- Messages favoris (fonctionnalité prévue)
- Gestion de différentes boîtes (fonctionnalité prévue)
- Recherche dans les conversations
- Filtrage des contacts

### 6.3 Responsive
- **Mobile**: Mode onglets (liste OU conversation)
- **Tablet**: 2 colonnes fixes
- **Desktop**: 3 colonnes avec sidebar détails

---

## 7. Module E-mails

### 7.1 Description
Client e-mail intégré pour la gestion des communications officielles.

### 7.2 Fonctionnalités

#### 7.2.1 Interface principale
**Layout 3 colonnes**:
- Sidebar boîtes/dossiers (gauche)
- Liste des e-mails (centre)
- Contenu de l'e-mail (droite)

#### 7.2.2 Gestion des boîtes
**Dossiers système**:
- Boîte de réception (compteur)
- Messages favoris (étoilés)
- Important (épinglés)
- Envoyés
- Brouillons (compteur)
- Archivés (compteur)
- Corbeille (compteur)

**Pour chaque dossier**:
- Icône distinctive
- Label
- Compteur de messages (si > 0)
- Sélection active avec highlight

#### 7.2.3 Nouveau message
**Dialog de composition**:
- Champ À: (destinataire email)
- Champ Objet
- Zone de contenu (textarea enrichie)
- Bouton joindre fichier
- Boutons Annuler/Envoyer
- Accessible via bouton principal

#### 7.2.4 Liste des e-mails
**Pour chaque e-mail**:
- Expéditeur (gras si non-lu)
- Objet (gras si non-lu)
- Preview du contenu (1 ligne)
- Timestamp
- Icônes:
  - Étoile (favoris) - jaune si actif
  - Trombone (pièce jointe)
- Highlight bleu si non-lu
- Sélection active avec fond accent
- Click pour ouvrir

#### 7.2.5 Visualisation d'e-mail
**Header**:
- Sujet en grand
- Expéditeur complet (nom + email)
- Timestamp
- Badge "Pièce jointe" si présent
- Boutons d'action:
  - Répondre
  - Répondre à tous
  - Transférer
  - Archiver
  - Supprimer

**Contenu**:
- Affichage du texte formaté
- Support paragraphes multiples
- Zone scrollable

#### 7.2.6 Fonctionnalités avancées
**Épinglage**:
- Marquage d'e-mails importants
- Accès rapide via dossier "Important"

**Favoris**:
- Système d'étoiles
- Dossier dédié "Messages favoris"

**Étiquettes/Labels**:
- Système de tags personnalisés
- Couleurs distinctives:
  - Urgent: Rouge
  - Formation: Bleu
  - Réglementation: Violet
  - Subvention: Vert
  - Culture: Jaune
- Affichage des labels sur les e-mails
- Filtrage par label

**Recherche**:
- Barre de recherche
- Recherche dans expéditeur et objet

#### 7.2.7 Actions groupées
- Archivage multiple
- Suppression multiple
- Marquage comme lu/non-lu
- Ajout/retrait favoris

### 7.3 Responsive
- **Mobile**: Stack vertical, navigation par onglets
- **Tablet**: 2 colonnes (dossiers + liste ou liste + contenu)
- **Desktop**: 3 colonnes complètes

---

## 8. Module Fichiers

### 8.1 Description
Gestionnaire de documents avec organisation par catégories, recherche et tri.

### 8.2 Fonctionnalités

#### 8.2.1 Vues d'affichage
**Vue Grille**:
- Cards avec icônes de fichiers
- Icône selon le type (PDF, DOC, XLSX, images, etc.)
- Nom du fichier
- Taille
- Propriétaire
- Badge catégorie
- Indicateur de partage (point vert)
- Actions au hover:
  - Télécharger
  - Partager
  - Menu d'options (Renommer, Supprimer)

**Vue Liste**:
- Tableau avec colonnes:
  - Icône + Nom
  - Catégorie
  - Taille
  - Propriétaire
  - Date de modification
  - Actions
- Headers de colonnes clairs
- Alignement optimal des données

#### 8.2.2 Téléchargement de fichiers
**Dialog d'upload**:
- Zone drag & drop
- Bouton "Parcourir"
- Sélection de catégorie (dropdown)
- Options:
  - Finances
  - Urbanisme
  - Administration
  - Communication
  - Archives
- Boutons Annuler/Télécharger

#### 8.2.3 Système de recherche et filtres
**Barre de recherche**:
- Recherche par nom de fichier
- Filtrage en temps réel

**Filtres**:
- Type de fichier (tous, PDF, documents, tableurs, images, archives)
- Tri par:
  - Nom (A-Z)
  - Date récente
  - Taille (du plus grand au plus petit)

#### 8.2.4 Types de fichiers supportés
**Icônes et couleurs par type**:
- PDF: Rouge, icône document
- DOC/DOCX: Bleu, icône document
- XLSX: Vert, icône tableur
- JPG/PNG: Violet, icône image
- MP4: Orange, icône vidéo
- ZIP: Gris, icône archive
- TXT: Gris, icône texte

#### 8.2.5 Gestion des fichiers
**Actions disponibles**:
- Télécharger un fichier
- Partager (indicateur visuel)
- Renommer
- Supprimer
- Visualiser les détails

**Métadonnées**:
- Nom
- Type/extension
- Taille
- Date de dernière modification
- Propriétaire
- Catégorie
- Statut de partage

#### 8.2.6 Système de catégories
Catégorisation par services:
- Finances
- Urbanisme
- Démographie
- Communication
- Administration
- Archives
- (Extensible)

#### 8.2.7 Fonctionnalités avancées (prévues)
- Système de dossiers hiérarchiques
- Permissions par fichier
- Versions de documents
- Preview intégrée
- Tri avancé multi-critères

### 8.3 Responsive
- **Mobile**: Vue grille 2 colonnes, actions simplifiées
- **Tablet**: Vue grille 3-4 colonnes
- **Desktop**: Vue grille 6 colonnes ou liste complète

---

## 9. Module Formation

### 9.1 Description
Plateforme e-learning pour les formations obligatoires et développement professionnel.

### 9.2 Fonctionnalités

#### 9.2.1 Catalogue de formations
**Affichage en grille**:
- Cards de formations (3 colonnes desktop)
- Pour chaque formation:
  - Image/thumbnail (gradient coloré)
  - Titre
  - Description courte
  - Instructeur
  - Note moyenne (étoiles)
  - Durée totale
  - Nombre de chapitres
  - Nombre d'étudiants
  - Niveau (Débutant/Intermédiaire/Avancé)
  - Statut (Non commencé/En cours/Terminé)
  - Badge "Obligatoire" si applicable
  - Barre de progression (si commencée)
  - Date d'échéance (si obligatoire)
  - Bouton CTA (Commencer/Continuer/Revoir)

#### 9.2.2 Filtrage des formations
**Barre de recherche**:
- Recherche par titre

**Filtres**:
- Catégorie:
  - Toutes
  - Sécurité
  - Administration
  - Communication
  - Finances
  - (Autres)
- Statut:
  - Tous
  - Non commencé
  - En cours
  - Terminé

#### 9.2.3 Niveaux de difficulté
**3 niveaux avec badges colorés**:
- Débutant: Vert
- Intermédiaire: Orange
- Avancé: Rouge

#### 9.2.4 Visualisation d'une formation
**Dialog détaillé** (modale plein écran):
- Zone vidéo (placeholder)
- Description complète
- Métadonnées:
  - Instructeur
  - Durée totale
  - Note + nombre d'étudiants
- Liste des chapitres:
  - Numérotation
  - Titre
  - Durée
  - Statut (complété ou non)
  - Icône checkmark si terminé
  - Hover effect
  - Zones différenciées (vert si complété)
- Barre de progression globale
- Bouton "Commencer le cours" / "Continuer"

#### 9.2.6 Statistiques du centre de formation
**4 cartes de stats**:
- Formations disponibles (total)
- En cours (nombre)
- Terminées (nombre)
- Certifications obtenues

**Affichage**:
- Grid responsive (2 colonnes mobile, 4 desktop)
- Icônes colorées
- Chiffres en évidence

#### 9.2.7 Types de contenu (extensions prévues)
Actuellement vidéo, à étendre:
- PDF
- Documents texte
- Quizz interactifs
- Présentations
- Ressources téléchargeables

#### 9.2.8 Système de suivi
- Progression par formation (%)
- Marquage automatique des chapitres
- Historique de complétion
- Certificats de réussite
- Échéances pour formations obligatoires

### 9.3 Responsive
- **Mobile**: 1 colonne, cartes optimisées
- **Tablet**: 2 colonnes
- **Desktop**: 3 colonnes, dialog optimisé

---

## 10. Module Calendrier

### 10.1 Description
Système de gestion d'événements et de planification avec vue calendrier.

### 10.2 Fonctionnalités

#### 10.2.1 Vues du calendrier
**3 modes**:
- Vue Mois (défaut)
- Vue Semaine
- Vue Jour

**Navigation**:
- Boutons Précédent/Suivant
- Affichage mois et année
- Sélecteur de vue (tabs)

#### 10.2.2 Vue Mois (détaillée)
**Grille calendaire**:
- Headers jours de semaine (Lun-Dim)
- Cases pour chaque jour du mois
- Highlight du jour actuel (bordure primaire, fond coloré)
- Pour chaque jour:
  - Numéro du jour
  - Événements du jour (max 2 visibles sur desktop, 1 sur mobile)
  - Badge coloré par catégorie
  - Titre tronqué
  - Indicateur "+X autre(s)" si plus d'événements
- Hover effect sur les cases
- Cases vides pour début/fin de mois

#### 10.2.3 Création d'événement
**Dialog "Nouvel événement"**:
- Titre (input)
- Description (textarea)
- Date (date picker)
- Catégorie (select):
  - Réunion
  - Échéance
  - Service public
  - Formation
  - Autre
- Heure de début (time picker)
- Heure de fin (time picker)
- Lieu (input)
- Boutons Annuler/Créer

#### 10.2.4 Catégories d'événements
**5 catégories avec couleurs**:
- Réunion: Bleu
- Échéance: Rouge
- Service public: Vert
- Formation: Violet
- Autre: Gris

#### 10.2.5 Sidebar événements à venir
**Liste chronologique**:
- Titre de l'événement
- Badge catégorie
- Date (icône calendrier)
- Horaires (icône horloge)
- Lieu (icône map pin)
- Nombre de participants si applicable
- Scroll si plus de 5 événements
- Tri du plus proche au plus lointain

#### 10.2.6 Statistiques rapides
**Card de stats**:
- Événements ce mois
- Événements cette semaine
- Événements aujourd'hui
- Chiffres mis en évidence

#### 10.2.7 Gestion des événements
**Actions disponibles**:
- Créer un événement
- Modifier un événement
- Supprimer un événement
- Voir les détails
- Filtrer par catégorie
- Rechercher dans les événements


### 10.3 Responsive
- **Mobile**: Calendrier compact, 1 événement par case
- **Tablet**: 2 événements par case
- **Desktop**: Layout 3:1 (calendrier:sidebar)

---

## 11. Module Paramètres

### 11.1 Description
Centre de configuration complète de l'application et du compte utilisateur.

### 11.2 Organisation
**6 onglets principaux**:
1. Profil
2. Sécurité
3. Notifications
4. Apparence
5. Général
6. Système

### 11.3 Onglet Profil

#### 11.3.1 Photo de profil
- Avatar actuel (initiales si pas de photo)
- Bouton "Changer la photo"
- Formats acceptés: JPG, PNG
- Taille max: 2MB

#### 11.3.2 Informations personnelles
**Formulaire (grid 2 colonnes)**:
- Nom complet
- Adresse e-mail
- Téléphone
- Service (dropdown):
  - Direction Générale
  - Finances
  - Urbanisme
  - Culture
  - Travaux
  - RH
- Poste/Fonction
- Biographie (textarea multi-lignes)

**Actions**:
- Bouton "Enregistrer les modifications"
- Séparateur visuel entre sections

### 11.4 Onglet Sécurité

#### 11.4.1 Changement de mot de passe
- Mot de passe actuel
- Nouveau mot de passe
- Confirmation du mot de passe
- Bouton "Changer le mot de passe"

#### 11.4.2 Authentification à deux facteurs
**2 méthodes**:
- SMS: Switch on/off avec description
- Application (Google Authenticator): Switch on/off

#### 11.4.3 Sessions actives
**Liste des sessions**:
- Session actuelle:
  - Point vert (active)
  - Navigateur et OS
  - Localisation
  - Badge "Actuelle"
- Autres sessions:
  - Point gris
  - Appareil et navigateur
  - Timestamp dernière activité
  - Bouton "Déconnecter"

### 11.5 Onglet Notifications

#### 11.5.1 Canaux de notification
**3 types avec switch**:
- E-mail: Notifications importantes par e-mail
- Push: Notifications instantanées navigateur
- Desktop: Notifications bureau

#### 11.5.2 Types de notifications
**Switches par module**:
- Messages: Nouveaux messages reçus
- Projets: Mises à jour des projets
- Calendrier: Rappels d'événements

**Présentation**:
- Description de chaque option
- Switch on/off
- Séparateurs visuels

### 11.6 Onglet Apparence

#### 11.6.1 Thème
**3 options (radio buttons)**:
- Clair (icône soleil)
- Sombre (icône lune)
- Système (icône moniteur)

**Affichage**:
- Cards avec bordure
- Icônes + labels
- Sélection visuelle

#### 11.6.2 Personnalisation
**Taille de police**:
- Slider 12-24px
- Labels: Petit / Normal / Grand
- Aperçu en temps réel

**Compacité**:
- Select dropdown:
  - Compact
  - Normal
  - Confortable

### 11.7 Onglet Général

#### 11.7.1 Langue et région
**Langue de l'interface**:
- Dropdown avec options:
  - Français
  - English
  - Español
  - Deutsch

**Fuseau horaire**:
- Select avec principales zones:
  - Europe/Paris (UTC+1)
  - Europe/London (UTC+0)
  - America/New_York (UTC-5)

**Format de date**:
- DD/MM/YYYY

#### 11.7.2 Démarrage
**Page d'accueil par défaut**:
- Select avec modules:
  - Tableau de bord
  - Projets
  - Calendrier
  - Messages

**Options supplémentaires**:
- Switch: Ouverture auto des notifications

### 11.8 Onglet Système

#### 11.8.1 Informations système
**Grid 2 colonnes**:
- Version de l'application: Mairie360 v2.1.0
- Dernière mise à jour: Date
- Navigateur: Chrome avec version
- Système d'exploitation: Windows/Mac/Linux

#### 11.8.2 Stockage et données
**Utilisation**:
- Barre de progression (utilisé/total)
- Indication 2.4 MB / 50 MB
- Bouton "Vider le cache"
- Description de l'action

#### 11.8.3 Assistance
**4 boutons**:
- Centre d'aide
- Contacter le support
- Signaler un problème
- Télécharger les logs

**Présentation**:
- Grid 2 colonnes
- Boutons outline avec texte aligné

### 11.9 Responsive
- **Mobile**: 2-4 onglets par ligne, stack vertical
- **Tablet**: 4 onglets par ligne
- **Desktop**: 6 onglets, layout optimisé

---

## 12. Layout et Navigation

### 12.1 Structure globale
**Composant Layout.tsx** encapsule toutes les pages.

### 12.2 Sidebar (Navigation principale)

#### 12.2.1 Éléments
**Header de sidebar**:
- Logo
- Nom "Mairie360"
- Bouton fermeture (mobile)

**Menu de navigation**:
- 8 liens principaux:
  1. Tableau de bord
  2. Projets
  3. Messagerie
  4. E-mails
  5. Fichiers
  6. Formation
  7. Calendrier
  8. Paramètres

#### 12.2.2 Comportement responsive
- **Mobile**: Sidebar cachée par défaut, overlay
  - Bouton hamburger pour ouvrir
  - Animation slide-in/out
- **Desktop**: Sidebar fixe, toujours visible

### 12.3 Header (Barre supérieure)

#### 12.3.1 Section gauche
- Bouton menu (mobile uniquement)
- Barre de recherche globale (desktop)

#### 12.3.2 Section droite
**3 éléments**:
- Icône recherche (mobile)
- Notifications
- Menu utilisateur (dropdown):
  - Avatar avec initiales
  - Nom utilisateur (desktop)
  - Menu déroulant:
    - Profil
    - Paramètres
    - Déconnexion

### 12.4 Footer

#### 12.4.1 Contenu
**2 sections**:
**Gauche**:
- Copyright © 2024 Mairie360
- Version 2.1.0
- Séparateurs (•)

**Droite**:
- Support technique (lien)
- Documentation (lien)
- Conditions d'utilisation (lien)
- Séparateurs (•)

#### 12.4.2 Style
- Bordure supérieure
- Padding adaptatif
- Texte muted
- Hover effects sur liens

#### 12.4.3 Responsive
- **Mobile**: Stack vertical, texte centré
- **Desktop**: Flexbox horizontal, justifié

---

## 13. Exigences techniques

### 13.1 Performance
- Rendu initial < 2 secondes
- Interactions fluides (60fps)
- Lazy loading des images
- Code splitting par module

### 13.2 Accessibilité
- Navigation au clavier
- Aria labels sur éléments interactifs
- Focus visible
- Lecture pour non voyant

### 13.3 Compatibilité
**Navigateurs supportés**:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

### 13.4 Sécurité
- Validation des inputs
- Protection XSS
- Authentification sécurisée
- Sessions avec timeout
- HTTPS obligatoire en production

### 13.5 Tests
**À implémenter**:
- Tests unitaires
- Tests d'intégration
- Tests de responsive
- Tests d'accessibilité

### 13.6 Documentation
- Code comments pour logique complexe
- README avec instructions setup
- Documentation composants réutilisables
- Guide de contribution
- Changelog des versions

---

## 14. Contacts et Support

**Équipe projet**: Direction technique Mairie360  
**Version**: 1.0  
**Date de dernière mise à jour**: Octobre 2024  

---

*Ce cahier des charges est un document vivant qui sera mis à jour régulièrement en fonction des évolutions du projet Mairie360.*
