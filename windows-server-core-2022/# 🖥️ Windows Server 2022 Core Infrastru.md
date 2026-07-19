# 🖥️ Windows Server 2022 Core Infrastructure

> Déploiement d'une infrastructure Windows Server 2022 Core simulant le système d'information d'une PME.

![Windows Server](https://img.shields.io/badge/Windows%20Server-2022-blue)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1+-5391FE)
![Active Directory](https://img.shields.io/badge/Active%20Directory-AD%20DS-green)
![Status](https://img.shields.io/badge/Status-Terminé-success)

---

# 📌 Présentation

Ce projet consiste à déployer une infrastructure complète sous **Windows Server 2022 Core** en environnement virtualisé.

L'objectif est de mettre en œuvre les principaux services d'une PME :

- Active Directory Domain Services
- DNS
- DHCP
- Gestion des utilisateurs
- Groupes de sécurité
- Partages SMB
- Sécurisation du domaine
- Administration PowerShell

L'ensemble de l'administration est réalisé **sans interface graphique (Server Core)**.

---

# 🎯 Objectifs

- Installer Windows Server 2022 Core
- Configurer un serveur avec une IP statique
- Déployer Active Directory
- Créer un domaine d'entreprise
- Configurer DNS
- Déployer DHCP
- Gérer les utilisateurs et groupes
- Créer des dossiers partagés sécurisés
- Mettre en place une politique de sécurité
- Administrer entièrement le serveur avec PowerShell

---

# 🏗️ Architecture

```
                     ENTREPRISE.LOCAL

                 +----------------------+
                 | Windows Server 2022  |
                 |      Server Core     |
                 +----------+-----------+
                            |
      ------------------------------------------------
      |              |               |               |
   Active         DNS            DHCP          SMB Shares
 Directory                                        |
                                                   |
                      -----------------------------
                      |             |             |
                    IT          COMPTA      DIRECTION
```

---

# 🛠 Technologies utilisées

- Windows Server 2022 Core
- PowerShell
- Active Directory Domain Services
- DNS
- DHCP
- SMB
- VirtualBox

---

# 📂 Fonctionnalités réalisées

## ✅ Configuration initiale

- Renommage du serveur
- Adresse IP statique
- Configuration DNS
- Vérification réseau

---

## ✅ Active Directory

- Installation du rôle AD DS
- Création du domaine

```
entreprise.local
```

- Promotion en contrôleur de domaine

---

## ✅ Gestion des utilisateurs

Création de :

- OU IT
- OU COMPTA
- OU DIRECTION

Création des groupes :

- GRP-IT
- GRP-COMPTA
- GRP-DIRECTION

Ajout des utilisateurs aux groupes correspondants.

---

## ✅ DHCP

Configuration de :

- plage d'adresses IP
- passerelle
- serveur DNS

Exemple :

```
192.168.1.100
↓

192.168.1.200
```

---

## ✅ Partages réseau

Création des partages :

```
IT
COMPTA
DIRECTION
```

avec des permissions basées sur les groupes Active Directory.

---

## ✅ Sécurité

- Politique de mot de passe
- Complexité obligatoire
- Verrouillage des comptes
- Permissions NTFS
- Permissions SMB

---

# 📸 Captures d'écran

Le dossier **/screenshots** contient notamment :

- Installation Server Core
- SCONFIG
- Adresse IP
- Installation AD DS
- Création du domaine
- Utilisateurs Active Directory
- Groupes
- Activation RDP
- Configuration DHCP
- Partages SMB
- Politique de sécurité

---

# 📁 Structure du projet

```
Windows-Server-Core/

│
├── README.md
├── Documentation/
│     └── Rapport.pdf
│
├── screenshots/
│     ├── 01-sconfig.png
│     ├── 02-ip.png
│     ├── 03-adds.png
│     ├── 04-ou.png
│     ├── 05-users.png
│     ├── 06-groups.png
│     ├── 07-rdp.png
│     ├── 08-dhcp.png
│     ├── 09-shares.png
│     └── 10-security.png
│
└── scripts/
      ├── ActiveDirectory.ps1
      ├── DHCP.ps1
      ├── Users.ps1
      └── Shares.ps1
```

---

# 💻 Compétences démontrées

- Administration Windows Server
- Active Directory
- DNS
- DHCP
- Gestion des utilisateurs
- Groupes de sécurité
- Permissions NTFS
- Partages SMB
- PowerShell
- Server Core
- Virtualisation
- Administration réseau

---

# 📖 Documentation

Une documentation complète du projet est disponible dans le dossier :

```
Documentation/
```

Elle détaille :

- les étapes du déploiement,
- les commandes PowerShell,
- les captures d'écran,
- les résultats obtenus.

---

# 🚀 Résultat

À l'issue du projet, l'infrastructure permet :

- une authentification centralisée ;
- une résolution de noms via DNS ;
- une attribution automatique des adresses IP ;
- des partages sécurisés par service ;
- une administration entièrement réalisée avec PowerShell.

