# Diagrammes de Séquence - MyDil-Model-EPSI

## 1. Flux d'Authentification

```mermaid
sequenceDiagram
    participant Utilisateur
    participant Application
    participant Système Auth
    participant Base de Données

    Utilisateur->>Application: Saisit email
    Application->>Système Auth: Vérifie domaine email

    alt Domaine autorisé
        Système Auth->>Système Auth: Détermine rôle<br/>(Étudiant/Formateur/Admin)
        Système Auth->>Base de Données: Enregistre/met à jour utilisateur
        Système Auth->>Application: Authentification réussie + Rôle
        Application->>Utilisateur: Redirection vers Dashboard
    else Domaine non autorisé
        Système Auth->>Application: Erreur authentification
        Application->>Utilisateur: Message: "Domaine non autorisé"
    end
```

## 2. Flux de Demande d'Emprunt (Étudiant)

```mermaid
sequenceDiagram
    participant Étudiant
    participant Application
    participant Base de Données
    participant Administrateur

    Étudiant->>Application: Consulte catalogue matériel
    Application->>Base de Données: Récupère liste matériel
    Base de Données->>Application: Retourne matériels disponibles
    Application->>Étudiant: Affiche catalogue avec filtres

    Étudiant->>Application: Sélectionne un matériel
    Application->>Base de Données: Récupère fiche matériel
    Base de Données->>Application: Retourne détails + historique
    Application->>Étudiant: Affiche fiche matériel

    Étudiant->>Application: Remplit formulaire emprunt<br/>(dates début/fin + motif)

    alt Matériel disponible
        Application->>Base de Données: Crée demande (statut: En attente)
        Base de Données->>Application: ID demande généré
        Application->>Étudiant: Succès: "Demande envoyée"
        Application->>Administrateur: Notifie nouvelle demande
    else Matériel indisponible
        Application->>Étudiant: Erreur: "Matériel indisponible"
    end
```

## 3. Flux de Validation de Demande (Administrateur)

```mermaid
sequenceDiagram
    participant Administrateur
    participant Application
    participant Base de Données
    participant Étudiant

    Administrateur->>Application: Accède au Dashboard Admin
    Application->>Base de Données: Récupère demandes en attente
    Base de Données->>Application: Retourne liste demandes
    Application->>Administrateur: Affiche demandes avec détails

    Administrateur->>Application: Consulte une demande
    Application->>Base de Données: Récupère détails demande
    Base de Données->>Application: Retourne infos complètes
    Application->>Administrateur: Affiche détails (dates, motif, etc.)

    alt Accepte la demande
        Administrateur->>Application: Clique "Accepter"
        Application->>Base de Données: Met à jour statut: "Acceptée"
        Application->>Base de Données: Met à jour disponibilité matériel
        Base de Données->>Application: Confirmation
        Application->>Étudiant: Notifie acceptation
        Application->>Administrateur: Succès: "Demande acceptée"
    else Refuse la demande
        Administrateur->>Application: Clique "Refuser"
        Application->>Base de Données: Met à jour statut: "Refusée"
        Base de Données->>Application: Confirmation
        Application->>Étudiant: Notifie refus
        Application->>Administrateur: Succès: "Demande refusée"
    end
```

## 4. Flux de Suivi d'Emprunt (Utilisateur)

```mermaid
sequenceDiagram
    participant Utilisateur
    participant Application
    participant Base de Données
    participant Système de Vérification

    Utilisateur->>Application: Accède à "Mes emprunts"
    Application->>Base de Données: Récupère emprunts utilisateur
    Base de Données->>Application: Retourne emprunts en cours + historique

    Application->>Système de Vérification: Vérifie retards
    Système de Vérification->>Base de Données: Récupère dates retour
    Base de Données->>Système de Vérification: Retourne dates
    Système de Vérification->>Application: Identifie retards

    Application->>Utilisateur: Affiche emprunts<br/>avec statut et alertes retard

    alt Emprunt en retard
        Application->>Utilisateur: Affiche notification retard
        Utilisateur->>Application: Signale le retour
        Application->>Base de Données: Enregistre retour
        Application->>Utilisateur: Succès: "Retour enregistré"
    else Emprunt dans les délais
        Utilisateur->>Application: Signale le retour
        Application->>Base de Données: Enregistre retour + état matériel
        Application->>Utilisateur: Succès: "Retour enregistré"
    end
```

## 5. Flux de Gestion des Retours (Administrateur)

```mermaid
sequenceDiagram
    participant Administrateur
    participant Application
    participant Base de Données
    participant Système Inventaire

    Administrateur->>Application: Accède aux retours en attente
    Application->>Base de Données: Récupère emprunts à retourner
    Base de Données->>Application: Retourne liste
    Application->>Administrateur: Affiche emprunts en retard/terminés

    Administrateur->>Application: Sélectionne un emprunt
    Administrateur->>Application: Enregistre l'état du matériel<br/>(Bon / Endommagé / Perdu)

    alt État Normal
        Application->>Base de Données: Met à jour statut emprunt: "Retourné"
        Application->>Base de Données: Met à jour disponibilité: "Disponible"
        Application->>Système Inventaire: Réinitialise matériel
    else État Endommagé
        Application->>Base de Données: Met à jour statut: "Retourné (Endommagé)"
        Application->>Base de Données: Met à jour état matériel: "Maintenance"
    else Matériel Perdu
        Application->>Base de Données: Met à jour statut: "Retourné (Perdu)"
        Application->>Base de Données: Met à jour matériel: "Non disponible"
    end

    Base de Données->>Application: Confirmation enregistrement
    Application->>Administrateur: Succès: "Retour enregistré"
```

## 6. Flux Complet (Vue Macroscopique)

```mermaid
sequenceDiagram
    participant Étudiant
    participant FormService as Service<br/>Application
    participant AdminService as Service<br/>Admin
    participant Database as Base de<br/>Données
    participant Notification as Système<br/>Notification

    Étudiant->>FormService: 1. Se connecte (email)
    FormService->>Database: Vérifie email + détermine rôle
    Database->>FormService: OK (Rôle: Étudiant)
    FormService->>Étudiant: Accès Dashboard

    Étudiant->>FormService: 2. Browse catalogue
    FormService->>Database: Récupère matériels
    Database->>FormService: Retourne liste
    FormService->>Étudiant: Affiche catalogue

    Étudiant->>FormService: 3. Demande emprunt (dates)
    FormService->>Database: Crée demande
    Database->>Notification: Notifie Admin
    FormService->>Étudiant: Succès

    Notification->>AdminService: Alert nouvelle demande
    AdminService->>Database: Récupère demande
    Database->>AdminService: Détails demande
    AdminService->>Database: 4. Accepte/Refuse
    Database->>Notification: Notifie résultat
    Notification->>Étudiant: Notification

    Étudiant->>FormService: 5. Suit emprunt
    FormService->>Database: Récupère statut
    Database->>FormService: OK + Date limite
    FormService->>Étudiant: Affiche emprunt

    Étudiant->>FormService: 6. Signale retour
    FormService->>Database: Enregistre retour
    Database->>AdminService: Demande confirmation
    AdminService->>Database: 7. Valide retour + état
    Database->>FormService: Confirmation
    FormService->>Étudiant: Succès: Retour enregistré
```
