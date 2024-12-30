# TDLOG Delivery Optimization Platform

## Description
Cette plateforme vise à optimiser les trajets de livraison pour les entreprises, en proposant des outils interactifs pour visualiser et recalculer les itinéraires sur une carte en temps réel. Le projet intègre un algorithme de calcul de chemin optimal, une base de données pour gérer les utilisateurs, et une interface utilisateur intuitive.

---

## Fonctionnalités Principales

1. **Système de connexion et d'inscription :**
   - Les utilisateurs peuvent créer un compte via la page d'inscription.
   - Les données des utilisateurs sont stockées dans une base de données SQLite3.
   - Une page de connexion sécurisée permet d'accéder à l'application.

2. **Carte interactive pour les itinéraires :**
   - Ajout dynamique de points de départ et d'arrivée directement sur la carte.
   - Calcul en temps réel des chemins optimaux via un algorithme dédié.
   - Représentation des chemins avec des flèches pour indiquer le sens du parcours.
   - Icônes pour identifier des étapes spécifiques sur le trajet.

3. **Option de réinitialisation :**
   - Réinitialisation complète de la carte pour repartir à zéro.

4. **Légende dynamique :**
   - Une légende claire pour interpréter les icônes et le parcours.
     


### Principe de l'Algorithme de Calcul des Chemins Optimaux

L'algorithme utilisé repose sur le **clustering K-Medoids**, une méthode robuste pour regrouper les points de livraison et optimiser les trajets. Voici un résumé de son fonctionnement :

        1. *Regroupement des Points** : 
        - Les points de livraison sélectionnés sont regroupés en **clusters** en fonction de leur proximité géographique. 
        - Chaque cluster est centré autour d’un **medoid**, un point réel parmi les données.

        2. *Optimisation Locale des Chemins** : 
        - Une fois les clusters définis, les chemins optimaux reliant les points de chaque cluster sont calculés.
        - Le medoid est utilisé comme point de départ et d’arrivée.

        3. *Calcul Dynamique** :
        - L’algorithme s’adapte en temps réel aux points sélectionnés par l’utilisateur et recalcule les chemins en conséquence.

        4. *Visualisation Intuitive** :
        - Les clusters et les chemins sont affichés sur la carte avec des flèches pour indiquer la direction et des icônes pour marquer les étapes.

    Cet algorithme garantit une gestion efficace des livraisons, réduisant les distances parcourues tout en restant robuste face aux données imprécises ou aux anomalies.

## Technologies Utilisées

- **Backend :** Django (Python)
  - Gestion des utilisateurs via `django.contrib.auth`.
  - Points de terminaison pour recalculer les routes et gérer les données utilisateur.
- **Frontend :** HTML, CSS, JavaScript (Leaflet.js pour la carte interactive).
- **Base de données :** SQLite3 pour stocker les informations des utilisateurs.
- **Bibliothèques :**
  - Leaflet.js pour les cartes interactives.
  - Leaflet-PolylineDecorator pour afficher les flèches de direction.
  - Font Awesome pour les icônes.

---

## Installation et Exécution

### Prérequis

- Python 3.8 ou plus.
- Django (peut être installé via pip).
- Navigateur web récent.

### Étapes d'installation:

1. Clonez le dépôt Git :
   ```bash
   git clone https://github.com/username/tdlog/delivery_platform.git
   cd tdlog/delivery_platform

2. step-by-step sur VS-Code: 

    les étapes d'execution sur VScode, 
    - après avoir extrait le code dans un dossier, ouvrez le, 
    (installez toutes les bibliothèques et outils nécessaires si jamais non installés, comme Django, Sklearn,.... )
    - une fois sur le fichier sur VS, ouvrez le terminal, et faites, "cd delivery_platform" puis normalement si tout est bon, vous aurez un chemin qui ressemble à "PS C:\Users\pc\Desktop\TDLOG\delivery_platform> " 
    - maintenant, écrivez dans le terminal, "python manage.py runserver" et suivez le lien vers le web, 
    - la première page d'authentification s'affiche, si jamais on vous demande un nom d'utilisateur et un mot de passe mettez, user_name: "0000" et mdp: "mohamed2002@@", puis login, si vous voulez créer un nouveau compte pour s'authentifier, il suffit juste d'aller sur la page de "signup" et procèdez à la création de votre compte puis revenez pour vous connecter avec vos nouveau coordonées. 
    - et là vous aurez une deuxième page qui affiche une carte "maps" réelle, sur laquelle y'a les chemin de livraison sur la région de BOUSKOURA (remarque j'ai changer la base de données, maintenant elle contenait toute la région de CASABLANCA), et dans l'algorithme j'ai changé le point de départ pour qu'il devient, "l'ECOLE CENTRALE CASABLANCA" par défaut de tout les livreurs, là notre école est l'entreprise qui veut livrer ces produits, comme indiqué sur la carte.
    - à partir de maintenant vous en tant que livreur vous pouvez séléctionner les points de livraisons dirctement sur la carte et cliquez sur "Calculate my direction" pour visualiser votre chemin de parcours et le trajet le plus optimal à suivre, puis vous pouvez repartir à 0 sur le calcul si vous souhaitez effectuer une autre livraison ou si jamais vous vous etre trompez sur dans la séléction des points de livraison dans la première. 
    - une legende en bas de la page est faite pour vous guider lors de votre trajet. 


### Forme générale du projet:

delivery_platform
├── manage.py                   # Script principal pour gérer les commandes Django
├── db.sqlite3                  # Base de données SQLite utilisée pour stocker les données
├── delivery_platform/          # Répertoire principal de l'application Django
│   ├── __init__.py             # Indique que ce dossier est un module Python
│   ├── settings.py             # Configuration principale du projet
│   ├── urls.py                 # Définit les routes URL pour le projet
│   ├── asgi.py                 # Interface ASGI pour les déploiements asynchrones
│   ├── wsgi.py                 # Interface WSGI pour le déploiement en production
├── delivery_app/               # Application principale pour la plateforme
│   ├── __init__.py             # Indique que ce dossier est un module Python
│   ├── admin.py                # Configuration pour le panneau d'administration Django
│   ├── apps.py                 # Configuration spécifique à l'application
│   ├── migrations/             # Scripts pour gérer les migrations de base de données
│   ├── models.py               # Définit les modèles de base de données
│   ├── views.py                # Logique des vues pour gérer les requêtes utilisateur
│   ├── urls.py                 # Définit les routes spécifiques à cette application
│   ├── forms.py                # Formulaires pour la connexion et l'inscription (optionnel)
│   ├── templates/              # Dossiers contenant les fichiers HTML
│   │   ├── login.html          # Page de connexion
│   │   ├── signup.html         # Page d'inscription
│   │   ├── itinerary.html      # Page principale pour optimiser les routes
└── README.md                   # Documentation du projet (optionnel)
Bonne découverte
