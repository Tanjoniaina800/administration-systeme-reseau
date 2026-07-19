<div align="center">

# 🐧 Mini Infrastructure Linux pour PME

### Déploiement et sécurisation d'un serveur Ubuntu Server en environnement virtualisé

Simulation d'une infrastructure Linux destinée à une petite entreprise, intégrant la configuration réseau, la sécurisation des accès, l'administration système et le déploiement d'un serveur Web sécurisé.


# 📖 Présentation

Ce projet consiste à concevoir une **mini infrastructure Linux** reproduisant les principaux services qu'une **PME** peut utiliser au quotidien.

L'objectif est de démontrer les compétences fondamentales d'un **Administrateur Systèmes Linux**, depuis l'installation du système jusqu'à la sécurisation complète du serveur.

Le projet a été réalisé sur **Ubuntu Server** dans un environnement virtualisé avec **Oracle VirtualBox** et administré exclusivement en ligne de commande. :contentReference[oaicite:0]{index=0}

---

# 🎯 Objectifs

- Installer Ubuntu Server
- Configurer le réseau
- Attribuer une adresse IP statique
- Gérer les utilisateurs et groupes Linux
- Configurer les permissions
- Sécuriser les accès SSH
- Déployer un pare-feu UFW
- Installer Apache2
- Héberger une page Web
- Sécuriser le serveur en HTTPS
- Automatiser certaines tâches avec Bash
- Surveiller les ressources système

---

# 🏗️ Architecture du projet

```text
                        INTERNET
                            │
                            │
                     Oracle VirtualBox
                            │
                    Ubuntu Server 26.04
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
      SSH                Apache2             UFW
        │                   │                   │
 Accès distant         Site Web HTTP/HTTPS  Filtrage réseau
        │
 Utilisateurs Linux
        │
 Scripts Bash
```

---

# 🚀 Fonctionnalités

## ✅ Installation d'Ubuntu Server

- Installation du système
- Configuration initiale
- Mise à jour des paquets

---

## 🌐 Configuration réseau

- Vérification de la connectivité
- Configuration IPv4
- Adresse IP statique avec Netplan
- Configuration DNS
- Test réseau

---

## 👤 Gestion des utilisateurs

- Création d'utilisateurs
- Création de groupes
- Attribution des groupes
- Vérification des permissions

---

## 🔐 Sécurisation SSH

Le serveur est administrable à distance grâce à **OpenSSH**.

Configuration réalisée :

- Installation du service SSH
- Désactivation de la connexion Root
- Vérification du service
- Connexion distante sécurisée

---

## 🛡 Pare-feu UFW

Configuration d'un pare-feu limitant les accès au strict nécessaire.

Ports autorisés :

| Port | Service |
|------|----------|
|22|SSH|
|80|HTTP|
|443|HTTPS|

---

## 🌍 Serveur Web Apache2

Déploiement d'un serveur Apache permettant d'héberger une page Web.

Fonctionnalités :

- Installation Apache
- Vérification du service
- Déploiement d'une page HTML
- Accès depuis un navigateur

---

## 🔒 HTTPS

Le serveur Web est sécurisé grâce à :

- OpenSSL
- Certificat auto-signé
- Activation du module SSL Apache
- Configuration automatique via un script Bash

---

## ⚙ Scripts Bash

Deux scripts ont été développés.

### setup-https-apache.sh

Automatise :

- installation Apache
- installation OpenSSL
- génération du certificat
- activation HTTPS
- ouverture du port 443

---

### monitor.sh

Permet de surveiller :

- CPU
- RAM
- Disque

---

# 📂 Structure du dépôt

```text
Mini-Infrastructure-Linux-PME/

│
├── README.md
│
├── Documentation/
│     └── Documentation_Technique.pdf
│
├── scripts/
│     ├── setup-https-apache.sh
│     └── monitor.sh
│
├── website/
│     └── index.html
│
├── screenshots/
│     ├── 01-virtualbox.png
│     ├── 02-installation.png
│     ├── 03-network.png
│     ├── 04-users.png
│     ├── 05-permissions.png
│     ├── 06-ssh.png
│     ├── 07-ufw.png
│     ├── 08-apache.png
│     ├── 09-https.png
│     └── 10-monitor.png
│
└── LICENSE
```

---

# 📸 Aperçu du projet

Le dossier **screenshots/** contient toutes les captures d'écran illustrant les différentes étapes du déploiement :

- Installation Ubuntu Server
- Configuration réseau
- Gestion des utilisateurs
- Permissions Linux
- SSH
- Pare-feu UFW
- Apache2
- HTTPS
- Scripts Bash
- Supervision système

---

# 🧰 Technologies utilisées

| Technologie | Utilisation |
|-------------|-------------|
|Ubuntu Server 26.04 LTS|Système d'exploitation|
|Oracle VirtualBox|Virtualisation|
|OpenSSH|Administration distante|
|Apache2|Serveur Web|
|UFW|Pare-feu|
|OpenSSL|HTTPS|
|Netplan|Configuration réseau|
|Bash|Automatisation|
|Nano|Édition de fichiers|

---

# 🎓 Compétences démontrées

Ce projet met en évidence les compétences suivantes :

- Administration Linux
- Gestion des utilisateurs
- Gestion des groupes
- Permissions Linux
- Configuration réseau
- Netplan
- SSH
- Apache2
- HTTPS
- UFW
- Bash Scripting
- Surveillance système
- Virtualisation
- Dépannage Linux

---

# 📚 Documentation

Une documentation technique complète accompagne ce projet.

Elle détaille :

- les étapes de déploiement ;
- les commandes utilisées ;
- les captures d'écran ;
- les scripts Bash ;
- les bonnes pratiques de sécurisation. :contentReference[oaicite:1]{index=1}

---

# 📈 Résultats obtenus

À la fin du projet, l'infrastructure permet :

- ✅ Administration distante via SSH
- ✅ Serveur Web Apache opérationnel
- ✅ Hébergement d'une page HTML
- ✅ Chiffrement HTTPS
- ✅ Pare-feu configuré
- ✅ Utilisateurs et groupes sécurisés
- ✅ Supervision des ressources système
- ✅ Scripts d'automatisation fonctionnels

---

# 👨‍💻 Auteur

**Silvano Tanjoniaina**

Étudiant en Informatique — Administration Systèmes & Réseaux

Projet personnel réalisé dans le cadre du développement de compétences en administration Linux et de la préparation à un stage.

---

<div align="center">

### ⭐ Si ce projet vous intéresse, n'hésitez pas à laisser une étoile sur le dépôt !

