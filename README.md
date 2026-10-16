# Epicur'App

Application de gestion pour restaurant gastronomique sans carte fixe : suivi des clients et de leurs allergies, composition des menus, historique des repas servis et préparation du service.

Projet réalisé dans le cadre de la **SAé 3.01** du BUT Informatique (IUT de Dijon), en équipe de 4, de septembre à décembre 2025.

## Fonctionnalités

- **Clients** : fiches clients, allergènes associés, historique des repas
- **Menus** : création et consultation des menus, association des plats et des invités
- **Boîte à idées** : idées de plats classées par catégorie
- **Étiquettes et liste de courses** : génération en PDF (iText)

## Architecture

```
EpicurApp/              Client lourd Windows
├── EpicurAppIHM/       Interface WPF (C#), appels à l'API via HttpClient
├── EpicurAPP-Partage/  Modèles et exceptions partagés client / API
└── deploiement.iss     Script d'installeur Windows (Inno Setup)

EpicurApp-API/          API REST
├── EpicurApp-API/      ASP.NET Core : contrôleurs, DAO, accès SQLite, Swagger, Dockerfile
├── EpicurAppLogic/     Services métier et interfaces
└── ClientServicesTest/ Tests unitaires des services métier
```

Architecture en couches : contrôleurs → services métier → DAO, avec injection de dépendances.

## Stack

C# / .NET 8 · WPF · ASP.NET Core · SQLite · Docker · Inno Setup · iText · Git/GitHub

## Lancer le projet

**API (Docker)**, depuis la racine du dépôt :

```bash
docker build -f EpicurApp-API/EpicurApp-API/Dockerfile -t epicurapp-api .
docker run -p 8081:8081 epicurapp-api
```

**API (local)** : ouvrir `EpicurApp-API/EpicurApp-API.sln` puis lancer le projet `EpicurApp-API` (Swagger disponible en environnement de développement).

**Client** : ouvrir `EpicurApp/EpicurApp-Client.sln` sous Windows et lancer `EpicurAppIHM`, ou utiliser l'installeur généré par `deploiement.iss`.

**Tests** : `dotnet test EpicurApp-API/ClientServicesTest`

## Équipe

Marwan Himeur · Romain Souveton · Louis Page · Augustin Bastide

Dépôt d'origine : [dept-info-iut-dijon/S3.01-C2_DinerParfait](https://github.com/dept-info-iut-dijon/S3.01-C2_DinerParfait)
