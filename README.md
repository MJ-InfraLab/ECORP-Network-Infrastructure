# 🌐 ECORP Enterprise Network Infrastructure

Projet de conception, de segmentation et de sécurisation d'une infrastructure réseau d'entreprise simulée sous **Cisco Packet Tracer** et **Debian Linux**.

---

## 📌 1. Vue d'ensemble de l'Architecture
Ce projet met en scène l'infrastructure de l'entreprise fictive *ECORP*, en simulant un environnement de production réel avec des services réseaux segmentés.

- **Switch principal** : `ECORP-SW01` (Configuration VLAN & SVI)
- **Routeur** : Routage inter-VLAN (*Router-on-a-Stick*)
- **Services Serveurs** : Résolution DNS locale (`www.ecorp.com`) et hébergement Web sous Debian.
- **Sécurité** : Administration distante durcie via **SSH v2** (chiffrement RSA 1024-bit), niveau de privilège 15, et bannissement de Telnet.

---

## ⚙️ 2. Réalisations Techniques & Dépannage

### A. Segmentation & Routage Inter-VLAN
* Création et nommage des VLANs d'administration et de trafic.
* Configuration des ports **Trunk** et des interfaces virtuelles de commutation (**SVI**) pour permettre la communication inter-VLAN via le routeur.
* Diagnostic et résolution des pannes de paquets ICMP (correction des pertes de paquets et des erreurs de routage).

### B. Services Réseau & Résolution DNS
* Configuration du serveur pour lier l'adresse IP du service Web au nom de domaine **`www.ecorp.com`**.
* Validation de bout en bout de la connectivité (Ping réussi et affichage du portail d'entreprise).

### C. Sécurisation de l'accès distant (SSH v2)
Extrait de la configuration appliquée sur le switch `ECORP-SW01` :

```cisco
ECORP-SW01(config)# hostname ECORP-SW01
ECORP-SW01(config)# ip domain-name ecorp.com
ECORP-SW01(config)# crypto key generate rsa
% How many bits in the modulus [512]: 1024
ECORP-SW01(config)# ip ssh version 2
ECORP-SW01(config)# line vty 0 15
ECORP-SW01(config-line)# transport input ssh
ECORP-SW01(config-line)# login local
