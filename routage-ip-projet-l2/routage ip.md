

# 🌐 Projet de Routage IP Inter-Domaines (RIPv2 & OSPF)

## 📌 Présentation du Projet
Ce projet d'infrastructure réseau consiste en la modélisation, la configuration et l'interconnexion de deux domaines de routage dynamique distincts (**RIPv2** et **OSPF**) avec mise en œuvre d'une **redistribution bidirectionnelle des routes**. 

Développé dans le cadre du cursus de **Licence Professionnelle en Informatique (Parcours Informatique Générale)** à l'**École Nationale d'Informatique (ENI) - Université de Fianarantsoa**, ce projet valide les compétences pratiques en administration système et réseau sous environnement virtuel et simulateur de topologies.

### 👥 Auteurs
* **RATELONIRAINY Mandaharitiana Sarobidy**
* **ALINARY Tanjoniaina Ricardo**
* **ZAFINDREMINDRAY Andrianampiansoa Valimbavaka Charly**
* **RANDRIAMALALA NAMPIHARIJAONA Tojo Fanieiana**
* *Année Universitaire : 2025-2026*

---

## 🛠️ Technologies & Environnement
* **Simulateur Réseau :** GNS3
* **Équipements :** Routeurs Cisco C7200 (Interfaces matérielles `C7200-IO-FE` sur le slot 0, `PA-8E` sur le slot 1)
* **Optimisation :** Configuration de la valeur `idle-PC` pour minimiser la consommation du processeur.
* **Analyse de Trames :** Wireshark (Capture de paquets réseau)

---

## 📐 Architecture & Configuration des Domaines

### 1. Domaine RIPv2 (Routing Information Protocol version 2)
* **Topologie :** Boucle de 6 routeurs (R1 à R6).
* **Adressage :** Sous-réseaux en `/24` allant de `192.168.1.0/24` à `192.168.6.0/24`.
* **Spécificités de Configuration :**
  * Activation de la `version 2` (support du routage sans classe - CIDR).
  * Désactivation de l'agrégation automatique via `no auto-summary`.
* **Tests de Résilience & Convergence :**
  * Simulation de panne par coupure de lien (`shutdown` entre R2 et R3) et suppression du nœud R2.
  * Analyse des mécanismes de temporisation internes de RIP (`Update`, `Invalid`, `Hold-down`, `Flush`).
  * Temps de convergence observé : environ **180 secondes (3 minutes)**.
  * Encapsulation des paquets de mise à jour : protocole de transport **UDP, port 520**.

### 2. Domaine OSPF (Open Shortest Path First)
* **Topologie :** Maillage de 3 routeurs (R7, R8, R9) intégrés au cœur de l'aire **Backbone (Area 0)**.
* **Adressage :** Sous-réseaux `192.168.7.0/24`, `192.168.8.0/24` et `192.168.9.0/24`.
* **Identifiants Stables (Router ID - RID) :** Configuration d'interfaces virtuelles **Loopback0** (`7.7.7.7`, `8.8.8.8`, `9.9.9.9`) garantissant la pérennité du RID face aux pannes d'interfaces physiques.
* **Mécanismes de Voisinage (Wireshark) :**
  * Échange de paquets **Hello** via l'adresse multicast **224.0.0.5**.
  * Fréquence des échanges : `Hello Interval` fixé à **10 secondes** / `Dead Interval` fixé à **40 secondes**.

---

## 🔄 Interconnexion & Redistribution Bidirectionnelle

Pour briser l'isolement des tables de routage et permettre la communication de bout en bout, une liaison d'interconnexion directe a été établie sur le sous-réseau `192.168.10.0/24` entre le routeur frontière **R4** (appartenant initialement au domaine RIP) et le routeur **R7** (domaine OSPF).

La configuration de la redistribution a été exécutée sur le routeur ASBR/frontière **R4** :

### Injection de RIP dans OSPF (RIP ➡️ OSPF)
Permet aux routeurs OSPF d'apprendre les routes du réseau RIP. Les routes importées apparaissent dans la table de routage de R8 sous la forme de routes externes de type 2 (**O E2**).
```cisconetwork
R4(config)# router ospf 1
R4(config-router)# redistribute rip subnets
```

### Injection d'OSPF dans RIP (OSPF ➡️ RIP)
Permet aux routeurs RIP d'apprendre les sous-réseaux et les adresses de loopback du domaine OSPF. Une métrique explicite doit être définie pour l'injection.
```cisconetwork
R4(config)# router rip
R4(config-router)# redistribute ospf 1 metric 1
```

---

## 🧪 Validation & Tests de Connectivité (`ping`)
* **Avant Redistribution :** Isolation complète. Un `ping` depuis R1 (RIP) vers la loopback de R8 (OSPF - `8.8.8.8`) échoue (taux de réussite de 0%).
* **Après Redistribution Bidirectionnelle :** Convergence globale réussie. Les tables de routage de R1 affichent désormais l'ensemble des routes OSPF sous l'indicateur `R` (avec une métrique cumulée). Les tests de ping de R1 vers `8.8.8.8` et de R8 vers `192.168.1.1` affichent un **Success rate de 100%**.
# 🌐 Projet de Routage IP Inter-Domaines (RIPv2 & OSPF)

## 📌 Présentation du Projet
Ce projet d'infrastructure réseau consiste en la modélisation, la configuration et l'interconnexion de deux domaines de routage dynamique distincts (**RIPv2** et **OSPF**) avec mise en œuvre d'une **redistribution bidirectionnelle des routes**. 

Développé dans le cadre du cursus de **Licence Professionnelle en Informatique (Parcours Informatique Générale)** à l'**École Nationale d'Informatique (ENI) - Université de Fianarantsoa**, ce projet valide les compétences pratiques en administration système et réseau sous environnement virtuel et simulateur de topologies.

### 👥 Auteurs
* **RATELONIRAINY Mandaharitiana Sarobidy**
* **ALINARY Tanjoniaina Ricardo**
* **ZAFINDREMINDRAY Andrianampiansoa Valimbavaka Charly**
* **RANDRIAMALALA NAMPIHARIJAONA Tojo Fanieiana**
* *Année Universitaire : 2025-2026*

---

## 🛠️ Technologies & Environnement
* **Simulateur Réseau :** GNS3
* **Équipements :** Routeurs Cisco C7200 (Interfaces matérielles `C7200-IO-FE` sur le slot 0, `PA-8E` sur le slot 1)
* **Optimisation :** Configuration de la valeur `idle-PC` pour minimiser la consommation du processeur.
* **Analyse de Trames :** Wireshark (Capture de paquets réseau)

---

## 📐 Architecture & Configuration des Domaines

### 1. Domaine RIPv2 (Routing Information Protocol version 2)
* **Topologie :** Boucle de 6 routeurs (R1 à R6).
* **Adressage :** Sous-réseaux en `/24` allant de `192.168.1.0/24` à `192.168.6.0/24`.
* **Spécificités de Configuration :**
  * Activation de la `version 2` (support du routage sans classe - CIDR).
  * Désactivation de l'agrégation automatique via `no auto-summary`.
* **Tests de Résilience & Convergence :**
  * Simulation de panne par coupure de lien (`shutdown` entre R2 et R3) et suppression du nœud R2.
  * Analyse des mécanismes de temporisation internes de RIP (`Update`, `Invalid`, `Hold-down`, `Flush`).
  * Temps de convergence observé : environ **180 secondes (3 minutes)**.
  * Encapsulation des paquets de mise à jour : protocole de transport **UDP, port 520**.

### 2. Domaine OSPF (Open Shortest Path First)
* **Topologie :** Maillage de 3 routeurs (R7, R8, R9) intégrés au cœur de l'aire **Backbone (Area 0)**.
* **Adressage :** Sous-réseaux `192.168.7.0/24`, `192.168.8.0/24` et `192.168.9.0/24`.
* **Identifiants Stables (Router ID - RID) :** Configuration d'interfaces virtuelles **Loopback0** (`7.7.7.7`, `8.8.8.8`, `9.9.9.9`) garantissant la pérennité du RID face aux pannes d'interfaces physiques.
* **Mécanismes de Voisinage (Wireshark) :**
  * Échange de paquets **Hello** via l'adresse multicast **224.0.0.5**.
  * Fréquence des échanges : `Hello Interval` fixé à **10 secondes** / `Dead Interval` fixé à **40 secondes**.

---

## 🔄 Interconnexion & Redistribution Bidirectionnelle

Pour briser l'isolement des tables de routage et permettre la communication de bout en bout, une liaison d'interconnexion directe a été établie sur le sous-réseau `192.168.10.0/24` entre le routeur frontière **R4** (appartenant initialement au domaine RIP) et le routeur **R7** (domaine OSPF).

La configuration de la redistribution a été exécutée sur le routeur ASBR/frontière **R4** :

### Injection de RIP dans OSPF (RIP ➡️ OSPF)
Permet aux routeurs OSPF d'apprendre les routes du réseau RIP. Les routes importées apparaissent dans la table de routage de R8 sous la forme de routes externes de type 2 (**O E2**).
```cisconetwork
R4(config)# router ospf 1
R4(config-router)# redistribute rip subnets
```

### Injection d'OSPF dans RIP (OSPF ➡️ RIP)
Permet aux routeurs RIP d'apprendre les sous-réseaux et les adresses de loopback du domaine OSPF. Une métrique explicite doit être définie pour l'injection.
```cisconetwork
R4(config)# router rip
R4(config-router)# redistribute ospf 1 metric 1
```

---

## 🧪 Validation & Tests de Connectivité (`ping`)
* **Avant Redistribution :** Isolation complète. Un `ping` depuis R1 (RIP) vers la loopback de R8 (OSPF - `8.8.8.8`) échoue (taux de réussite de 0%).
* **Après Redistribution Bidirectionnelle :** Convergence globale réussie. Les tables de routage de R1 affichent désormais l'ensemble des routes OSPF sous l'indicateur `R` (avec une métrique cumulée). Les tests de ping de R1 vers `8.8.8.8` et de R8 vers `192.168.1.1` affichent un **Success rate de 100%**.
# 🌐 Projet de Routage IP Inter-Domaines (RIPv2 & OSPF)

## 📌 Présentation du Projet
Ce projet d'infrastructure réseau consiste en la modélisation, la configuration et l'interconnexion de deux domaines de routage dynamique distincts (**RIPv2** et **OSPF**) avec mise en œuvre d'une **redistribution bidirectionnelle des routes**. 

Développé dans le cadre du cursus de **Licence Professionnelle en Informatique (Parcours Informatique Générale)** à l'**École Nationale d'Informatique (ENI) - Université de Fianarantsoa**, ce projet valide les compétences pratiques en administration système et réseau sous environnement virtuel et simulateur de topologies.

### 👥 Auteurs
* **RATELONIRAINY Mandaharitiana Sarobidy**
* **ALINARY Tanjoniaina Ricardo**
* **ZAFINDREMINDRAY Andrianampiansoa Valimbavaka Charly**
* **RANDRIAMALALA NAMPIHARIJAONA Tojo Fanieiana**
* *Année Universitaire : 2025-2026*

---

## 🛠️ Technologies & Environnement
* **Simulateur Réseau :** GNS3
* **Équipements :** Routeurs Cisco C7200 (Interfaces matérielles `C7200-IO-FE` sur le slot 0, `PA-8E` sur le slot 1)
* **Optimisation :** Configuration de la valeur `idle-PC` pour minimiser la consommation du processeur.
* **Analyse de Trames :** Wireshark (Capture de paquets réseau)

---

## 📐 Architecture & Configuration des Domaines

### 1. Domaine RIPv2 (Routing Information Protocol version 2)
* **Topologie :** Boucle de 6 routeurs (R1 à R6).
* **Adressage :** Sous-réseaux en `/24` allant de `192.168.1.0/24` à `192.168.6.0/24`.
* **Spécificités de Configuration :**
  * Activation de la `version 2` (support du routage sans classe - CIDR).
  * Désactivation de l'agrégation automatique via `no auto-summary`.
* **Tests de Résilience & Convergence :**
  * Simulation de panne par coupure de lien (`shutdown` entre R2 et R3) et suppression du nœud R2.
  * Analyse des mécanismes de temporisation internes de RIP (`Update`, `Invalid`, `Hold-down`, `Flush`).
  * Temps de convergence observé : environ **180 secondes (3 minutes)**.
  * Encapsulation des paquets de mise à jour : protocole de transport **UDP, port 520**.

### 2. Domaine OSPF (Open Shortest Path First)
* **Topologie :** Maillage de 3 routeurs (R7, R8, R9) intégrés au cœur de l'aire **Backbone (Area 0)**.
* **Adressage :** Sous-réseaux `192.168.7.0/24`, `192.168.8.0/24` et `192.168.9.0/24`.
* **Identifiants Stables (Router ID - RID) :** Configuration d'interfaces virtuelles **Loopback0** (`7.7.7.7`, `8.8.8.8`, `9.9.9.9`) garantissant la pérennité du RID face aux pannes d'interfaces physiques.
* **Mécanismes de Voisinage (Wireshark) :**
  * Échange de paquets **Hello** via l'adresse multicast **224.0.0.5**.
  * Fréquence des échanges : `Hello Interval` fixé à **10 secondes** / `Dead Interval` fixé à **40 secondes**.

---

## 🔄 Interconnexion & Redistribution Bidirectionnelle

Pour briser l'isolement des tables de routage et permettre la communication de bout en bout, une liaison d'interconnexion directe a été établie sur le sous-réseau `192.168.10.0/24` entre le routeur frontière **R4** (appartenant initialement au domaine RIP) et le routeur **R7** (domaine OSPF).

La configuration de la redistribution a été exécutée sur le routeur ASBR/frontière **R4** :

### Injection de RIP dans OSPF (RIP ➡️ OSPF)
Permet aux routeurs OSPF d'apprendre les routes du réseau RIP. Les routes importées apparaissent dans la table de routage de R8 sous la forme de routes externes de type 2 (**O E2**).
```cisconetwork
R4(config)# router ospf 1
R4(config-router)# redistribute rip subnets
```

### Injection d'OSPF dans RIP (OSPF ➡️ RIP)
Permet aux routeurs RIP d'apprendre les sous-réseaux et les adresses de loopback du domaine OSPF. Une métrique explicite doit être définie pour l'injection.
```cisconetwork
R4(config)# router rip
R4(config-router)# redistribute ospf 1 metric 1
```

---

## 🧪 Validation & Tests de Connectivité (`ping`)
* **Avant Redistribution :** Isolation complète. Un `ping` depuis R1 (RIP) vers la loopback de R8 (OSPF - `8.8.8.8`) échoue (taux de réussite de 0%).
* **Après Redistribution Bidirectionnelle :** Convergence globale réussie. Les tables de routage de R1 affichent désormais l'ensemble des routes OSPF sous l'indicateur `R` (avec une métrique cumulée). Les tests de ping de R1 vers `8.8.8.8` et de R8 vers `192.168.1.1` affichent un **Success rate de 100%**.