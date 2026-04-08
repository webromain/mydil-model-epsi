# Web App MyDil-Model-EPSI

## I - Gestion :

- Inventaire (stock)
- Matériel prêté (à qui, quand, état, retards)
- Tracabilité (historique, retours, maintenance)

---

## II - Connexions :

- Mails autorisés (voir sujet)

---

## III - Acteurs :

- Etudiant
- Formateur
- Administration

---

## IV - Besoins fonctionnels (utilisateurs & administrateurs) :

- Utilisateur peut créer une requête (d'enprunt)
- Utilisateur peut signaler le rendu
- Utilisateur peut répondre à une notification de retard
- Utilisateur peut voir la liste des objets disponibles

- Administrateur peut accepter ou refuser une demande
- Administrateur peut voir tous les emprunts et demandes
- Administrateur peut envoyer des rappels

---

## V - User Stories

### Étudiant :

- En tant qu’étudiant, je veux me connecter avec mon adresse email autorisée afin d’accéder à l’application.

- En tant qu’étudiant, je veux consulter le catalogue du matériel disponible afin de trouver un équipement adapté à mon besoin.

- En tant qu’étudiant, je veux filtrer le matériel (type, disponibilité, état) afin de gagner du temps dans ma recherche.

- En tant qu’étudiant, je veux faire une demande de prêt en indiquant une date de début et de fin afin de réserver un matériel.

- En tant qu’étudiant, je veux consulter mes prêts en cours et passés afin de suivre mes échéances et éviter les retards.

- En tant qu’étudiant, je veux recevoir une notification en cas de retard afin d’être informé rapidement.

### Formateur :

- En tant que formateur, je veux me connecter avec mon adresse email autorisée afin d’accéder à mes fonctionnalités.

- En tant que formateur, je veux consulter l’inventaire complet afin de vérifier la disponibilité du matériel pour mes cours.

- En tant que formateur, je veux effectuer une demande de prêt pour moi-même ou pour un groupe afin de préparer une séance pédagogique.

- En tant que formateur, je veux consulter l’historique d’un matériel afin de vérifier son état et son utilisation passée.

### Administration :

- En tant qu’administrateur autorisé, je veux accéder au dashboard d’administration afin de gérer les demandes de prêt.

- En tant qu’administrateur, je veux valider ou refuser une demande de prêt afin de contrôler l’attribution du matériel.

- En tant qu’administrateur, je veux enregistrer le retour d’un matériel et son état afin d’assurer la traçabilité.

- En tant qu’administrateur, je veux visualiser les retards en cours afin de relancer les utilisateurs concernés.

- En tant qu’administrateur, je veux ajouter, modifier ou retirer du matériel dans l’inventaire afin de maintenir le stock à jour.

- En tant qu’administrateur, je veux refuser automatiquement l’accès au rôle Administration si le compte n’est pas autorisé afin de sécuriser l’application.

---

## VI - Objectif du MVP

Permettre la gestion simple des emprunts de matériel avec :

- authentification sécurisée par domaine email
- consultation du stock
- création et validation des demandes
- suivi des emprunts et retards

### Authentification & Rôles

- Connexion par email uniquement
- Vérification automatique du domaine autorisé :
  - @mail-formateur.net
  - @ecoles-epsi.net
  - @competences-developpement.fr
- Attribution automatique du rôle selon le domaine
- Refus d’accès si domaine non autorisé

### Catalogue & Stock

- Affichage de la liste du matériel
- Indication de disponibilité (Disponible / Indisponible)
- Filtres simples (type + disponibilité)
- Fiche matériel basique (description + état)

### Demande d’Emprunt

- Formulaire avec :
  - Date de début
  - Date de fin
- Envoi de la demande
- Statut de la demande :
  - En attente
  - Acceptée
  - Refusée

### Gestion des Emprunts (Utilisateur)

- Page “Mes emprunts”
- Visualisation des statuts
- Indication des retards
- Bouton “Signaler un retour”

### Gestion Administration

- Dashboard simple :
  - Liste des demandes en attente
  - Liste des emprunts en cours
  - Retards
- Actions possibles :
  - Valider une demande
  - Refuser une demande
  - Enregistrer un retour

### Hors MVP (Version ultérieure)

- Statistiques avancées
- Gestion maintenance détaillée
- Notifications automatiques par email
- Historique complet exportable
- Gestion avancée des incidents

---

## VI - Sitemap

### Authentification

- Page de connexion
  - Saisie email
  - Vérification domaine autorisé :
    - @mail-formateur.net
    - @ecoles-epsi.net
    - @competences-developpement.fr
  - Attribution automatique du rôle selon le domaine :
    - Étudiant
    - Formateur
    - Administration
  - Messages système :
    - Erreur : domaine non autorisé
    - Erreur : accès administration refusé
    - Succès : connexion validée

### Espace Étudiant

#### Dashboard

- Vue synthèse :
  - Mes prêts en cours
  - Retards éventuels
  - Notifications

#### Catalogue matériel

- Liste des objets disponibles
- Filtres :
  - Type
  - Disponibilité
  - État
- Fiche matériel :
  - Description
  - État
  - Disponibilité
  - Historique simplifié

#### Demande d’emprunt

- Formulaire :
  - Dates début / fin
  - Motif
- Confirmation :
  - Succès (demande envoyée)
  - Erreur (matériel indisponible)

#### Mes emprunts

- Emprunts en cours
- Historique
- Détail d’un emprunt
- Signaler un rendu
- Répondre à une notification de retard

### Espace Formateur

#### Dashboard

- Vue synthèse :
  - Mes emprunts
  - Planning matériel
  - Notifications

#### Inventaire complet

- Liste complète du stock
- Filtres avancés
- Fiche matériel :
  - Informations détaillées
  - Historique complet
  - Maintenance

#### Demande d’emprunt

- Formulaire :
  - Pour soi
  - Pour un groupe
- Confirmation

#### Mes emprunts

- En cours
- Historique
- Signalement de retour

### Espace Administration

#### Dashboard Administration

- Demandes en attente
- Tous les emprunts
- Retards
- Alertes
- Statistiques stock

#### Gestion des demandes

- Valider une demande
- Refuser une demande
- Détail d’une demande

#### Gestion des retours

- Enregistrer un retour
- État du matériel au retour
- Déclarer incident

#### Gestion inventaire (Stock)

- Ajouter matériel
- Modifier matériel
- Supprimer matériel
- Mettre à jour état
- Gérer maintenance

#### Traçabilité

- Historique par matériel
- Historique par utilisateur
- Journal des actions

### États UX globaux

- Succès :
  - Demande envoyée
  - Retour enregistré
- Erreurs :
  - Domaine non autorisé
  - Matériel indisponible
  - Action non autorisée
- États vides :
  - Aucun matériel disponible
  - Aucune demande en attente
  - Aucun retard

---

## VII - Pages clés

### Page de Connexion

- Saisie de l’email
- Vérification du domaine autorisé
- Attribution automatique du rôle (Étudiant / Formateur / Administration)
- Messages d’erreur :
  - Domaine non autorisé
  - Accès administration refusé
- Message de succès (connexion validée)

### Catalogue Matériel (Liste + Filtres)

- Liste des objets disponibles
- Filtres :
  - Type
  - Disponibilité
  - État
- Indicateur visuel de disponibilité
- Message état vide : “Aucun matériel disponible”

### Fiche Matériel

- Nom du matériel
- Description
- État actuel
- Disponibilité
- Historique (emprunts / retours / maintenance)
- Bouton “Faire une demande de prêt”

### Demande d’Emprunt

- Sélection du matériel
- Dates de début et de fin
- Motif (optionnel ou obligatoire selon règle)
- Bouton d’envoi
- Message de succès : “Demande envoyée”
- Message d’erreur : matériel indisponible

### Mes Emprunts / Mes Demandes

- Emprunts en cours
- Historique des emprunts
- Statut :
  - En attente
  - Accepté
  - Refusé
  - En retard
  - Terminé
- Bouton “Signaler un retour”
- Notification de retard

### Dashboard Administration

- Vue globale :
  - Demandes en attente
  - Emprunts en cours
  - Retards
- Accès rapide :
  - Valider / Refuser une demande
  - Enregistrer un retour
  - Envoyer un rappel
- Indicateurs stock et alertes

---

## VIII - Wireframes (pj-figma)

### Pages

1. Connexion + choix rôle
2. Catalogue matériel (avec filtres)
3. Formulaire demande de prêt
4. Fiche matériel (infos + historique)
5. Dashboard Administration (demandes, alertes)
6. Retours (enregistrer retour + état)

### Obligation consigne

Sur au moins 2 pages, montrer :
● succès (“Demande envoyée”)
● erreur (“Domaine non autorisé” / “Rôle admin refusé”)
● vide (“Aucun matériel disponible”)

---

## VIV - Étude de cas / livraison

### Livrable 1 : Mini-dossier (PDF)

Doit contenir :

● Contexte + acteurs
● User stories
● MVP
● Navigation globale
● Captures des wireframes (Figma/Whimsical/Wireframe.cc)
● Justification UX (2–3 choix : filtres, statuts, parcours)

### Livrable 2 : Présentation orale

Plan conseillé :

1. Problème & objectifs
2. MVP
3. Navigation
4. 2–3 écrans expliqués
5. Choix UX + contraintes (rôles, domaines email)
