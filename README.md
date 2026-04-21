# Systeme-de-Gestion-de-Presence
 
![Système de Gestion de Présence](banner.png)
 
## Aperçu
 
Ce **Système de Gestion de Présence des Étudiants** basé sur Python est un outil conçu pour les établissements scolaires, les enseignants et les administrateurs. Il automatise le suivi des présences en combinant la **reconnaissance faciale** et la **géolocalisation GPS**, garantissant une détection de présence fiable et infalsifiable.
 
En s'appuyant sur `DeepFace` / `face_recognition` pour l'identification des visages, `OpenCV` pour la capture vidéo en temps réel, et `geopy` pour la vérification de la zone GPS, ce système offre une approche complète et intelligente de la gestion des présences. Les résultats sont stockés dans une base de données et accessibles via un tableau de bord interactif pour les enseignants et les administrateurs.
 
---
 
## Fonctionnalités
 
- **Reconnaissance Faciale** : identifie automatiquement chaque étudiant via la caméra.
- **Détection de Vivacité** : empêche la fraude en distinguant un vrai visage d'une photo (clignement des yeux, mouvement de la tête).
- **Géolocalisation GPS** : vérifie que l'étudiant se trouve physiquement dans la zone de la salle de classe (rayon : ~50m).
- **Tableau de Bord en Temps Réel** : l'enseignant suit les présences en direct pendant le cours.
- **Alertes Automatiques** : envoi de notifications par email/SMS aux étudiants absents ou à leurs parents.
- **Statistiques de Présence** : suivi du taux de présence par étudiant, par cours et par semaine.
- **Alerte de Seuil d'Absence** : déclenchement automatique d'une alerte quand un étudiant dépasse X absences.
- **Export de Rapports** : génération de rapports PDF ou Excel pour l'administration.
- **Mode Hors-ligne** : stockage local des données en cas de panne réseau, puis synchronisation au retour de la connexion.
- **Reconnaissance en Groupe** : détection de plusieurs visages simultanément depuis une seule photo de la salle.
---
 
## Architecture du Système
 
```
Étudiant (Application Mobile / Web)
              |
     Photo + Coordonnées GPS
              |
              v
     Backend Python (FastAPI)
       /               \
   DeepFace           Geopy
(Identification)   (Vérif. Zone)
       \               /
              v
   Base de Données (PostgreSQL / MongoDB)
              |
              v
  Tableau de Bord Enseignant & Admin
```
 
---
 
## Prérequis
 
- Python 3.x
- Une webcam ou caméra mobile
- Appareil avec GPS activé (smartphone ou navigateur)
- Instance PostgreSQL ou MongoDB
---
 
## Bibliothèques
 
### 👤 Reconnaissance Faciale
| Bibliothèque | Utilité |
|---|---|
| `face_recognition` | Détection et identification simple des visages |
| `DeepFace` | Modèles avancés (ArcFace, FaceNet) + détection d'émotions |
| `OpenCV (cv2)` | Capture vidéo et traitement d'image en temps réel |
| `dlib` | Détection des points caractéristiques du visage |
| `InsightFace` | Reconnaissance haute précision pour la production |
 
### 📍 Géolocalisation
| Bibliothèque | Utilité |
|---|---|
| `geopy` | Calcul de distance GPS entre deux coordonnées |
| `shapely` | Définir et vérifier si un point est dans une zone géographique |
| `folium` | Visualisation de cartes interactives |
 
### 🌐 Backend / API
| Bibliothèque | Utilité |
|---|---|
| `FastAPI` | API REST rapide et moderne |
| `Flask` | API légère, idéale pour le prototypage |
| `Django` | Framework complet avec gestion des utilisateurs intégrée |
 
### 🗄️ Base de Données
| Bibliothèque | Utilité |
|---|---|
| `SQLAlchemy` | ORM universel (PostgreSQL, MySQL, SQLite) |
| `pymongo` | MongoDB NoSQL (idéal pour stocker les vecteurs de visages encodés) |
| `Redis` | Cache rapide pour les sessions en temps réel |
 
### 📲 Notifications
| Bibliothèque | Utilité |
|---|---|
| `smtplib` | Envoi d'emails natif Python |
| `twilio` | SMS et appels automatiques |
| `firebase-admin` | Notifications push mobiles |
 
---
 
## Installation
 
Installez les dépendances requises avec les commandes suivantes :
 
```bash
pip install face_recognition
pip install deepface
pip install opencv-python
pip install geopy
pip install shapely
pip install fastapi uvicorn
pip install sqlalchemy
pip install pymongo
pip install twilio
pip install firebase-admin
pip install pandas openpyxl
```
 
---
 
## Sécurité & Mesures Anti-Fraude
 
- **Détection de Vivacité** — empêche l'utilisation d'une photo à la place d'un vrai visage
- **Rayon GPS Strict** — tout pointage effectué hors de la zone définie est automatiquement rejeté
- **Horodatage Signé** — chaque enregistrement de présence contient un timestamp infalsifiable
- **Double Vérification** — reconnaissance faciale + GPS + heure exacte du cours doivent tous correspondre
- **Détection d'Anomalies** — signale les comportements suspects (ex : pointage depuis une localisation impossible)
---
 
## Conclusion
 
Clonez le dépôt et configurez votre environnement :
 
```bash
git clone https://github.com/votre-nom/Systeme-de-Gestion-de-Presence.git
cd Systeme-de-Gestion-de-Presence
chmod -R +x scripts/
pip install -r requirements.txt
```
 
> ⚠️ Cet outil est destiné à un **usage éducatif et administratif uniquement**. Obtenez toujours le consentement approprié avant de collecter des données biométriques, conformément aux réglementations locales sur la vie privée (RGPD, et
