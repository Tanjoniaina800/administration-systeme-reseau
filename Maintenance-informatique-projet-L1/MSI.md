# Maintenance Windows à Distance : Approche Hybride Graphique et Ligne de Commande

Ce dépôt centralise les scripts, les stratégies d'exécution et les guides opérationnels développés dans le cadre du module **Maintenance des systèmes informatiques** (Année universitaire 2024-2025). Ce framework combine l'interface graphique de **TeamViewer** et l'automatisation en ligne de commande via **Sysinternals PsExec**.

---

## 👥 Membres du Projet & Informations
*   **Étudiants :**
    *   RATELONYRAINY Mandaharitiana Sarobidy (2466H-F)
    *   RANDRIANIRINA Albert (2379H-F)
    *   ANDRIAMAHARO Salohiniaina Cyrille (2366H-F)
    *   ALINARY Tanjoniaina Ricardo (2467H-F)
*   **Encadrant :** RAZAFINDRAIBE Marolahy Alix
*   **Année universitaire :** 2024-2025
*   **Matière :** Maintenance des systèmes informatiques

---

## 🎯 Présentation du Projet
La maintenance moderne des parcs informatiques exige agilité, sécurité renforcée et un impact minimal sur la productivité des utilisateurs[cite: 1]. Ce projet valide une **architecture hybride** pour l'administration distante de postes Windows[cite: 1] :
1. **Contrôle Interactif (GUI) :** Utilisation de **TeamViewer** (en exploitant le Mode LAN et l'authentification Windows native) pour les interventions manuelles nécessitant une vérification visuelle[cite: 1].
2. **Automatisation Silencieuse (CLI) :** Utilisation de **PsExec (v2.43)** pour exécuter des scripts, des installateurs et des commandes système directement en arrière-plan, sans perturber l'utilisateur ni ouvrir de session de bureau complète[cite: 1].

### 📈 Résultats Obtenus
*   **Réduction du temps d'intervention :** Exécution instantanée des tâches récurrentes[cite: 1].
*   **Automatisation des tâches répétitives :** Diminution des actions manuelles chronophages[cite: 1].
*   **Intervention non intrusive :** Exécution en arrière-plan sans blocage de l'interface utilisateur[cite: 1].
*   **Sécurité renforcée :** Opérations exécutées à distance à l'aide d'identifiants explicites Windows sans session visible[cite: 1].

---

## 🛠️ Fonctionnalités Techniques Clés

### 1. Administration Sécurisée des Postes
*   **Mode LAN TeamViewer :** Configuration de sessions visuelles directes via les sous-réseaux locaux pour s'affranchir de la connexion Internet[cite: 1].
*   **Authentification Windows :** Connexion directe en utilisant les identifiants d'administration (locaux ou domaine) au lieu des mots de passe dynamiques de TeamViewer[cite: 1].
*   **Gestion des Comptes en CLI :** Modification sécurisée du mot de passe d'un utilisateur à distance via `PsExec`[cite: 1] :
    ```cmd
    psexec \\<IP_Distante> -u <Utilisateur> -p <Ancien_Mot_De_Passe> net user <Utilisateur> <Nouveau_Mot_De_Passe>
    ```

### 2. Nettoyage et Optimisation Automatisés
Combinaison d'outils visuels (`msconfig`, `cleanmgr`) et d'un script batch silencieux via `PsExec` pour purger les fichiers temporaires (`%TEMP%`, `C:\Windows\Temp`) et arrêter les services superflus ou lourds[cite: 1].

### 3. Gestion Sauvegarde/Restauration du Registre
Sauvegarde et restauration distantes de clés de registre critiques à l'aide des commandes natives `reg export` et `reg import` intégrées à l'infrastructure `PsExec`[cite: 1].

### 4. Déploiement Silencieux de Logiciels
Transfert préalable des packages via le module de transfert de fichiers de TeamViewer, suivi de leur installation automatisée avec arguments silencieux (`/S`) via `PsExec`[cite: 1].

---

## 💾 Scripts Principaux

### 📁 `scripts/nettoyage-auto.bat`
Ce script d'optimisation nettoie le système et désactive les processus réseau ou de télémétrie obsolètes/lourds afin de libérer de la mémoire et du CPU[cite: 1].

```batch
@echo off
:: Script de Maintenance Windows - Nettoyage Distant
:: Purge silencieuse des répertoires temporaires système et utilisateur

del /q /f %TEMP%\*
del /q /f c:\Windows\Temp\*

:: Arrêt de la télémétrie, de SuperFetch et des services inutilisés
net stop "DiagTrack"
net stop "Sysmain"
net stop "Fax"

echo Nettoyage et optimisation système terminés avec succès.