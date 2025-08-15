# Configuration de VirtualBox pour le laboratoire

Ce document explique comment créer et configurer chaque machine virtuelle du laboratoire de cybersécurité.

## 1. Création des machines virtuelles
Ouvrir VirtualBox → Cliquer sur "Nouvelle" → Choisir un nom clair (ex: `Kali`, `IPFire`, `SELKS`, `WindowsServer`).

---

### Kali Linux (Attaquant)
- **OS** : Linux → Debian (64-bit)
- **RAM** : 4 Go minimum
- **Stockage** : 40 Go
- **Adaptateurs réseau** :
  - Adaptateur 1 : Réseau interne → LAB_RED
  - Adaptateur 2 : NAT *(optionnel)*

---

### pfSense (Pare-feu / Routeur)
- **OS** : Linux → Autre (64-bit)
- **RAM** : 1 Go
- **Stockage** : 4 Go
- **Adaptateurs réseau** :
  - Adaptateur 1 : Réseau interne → LAB_RED (RED)
  - Adaptateur 2 : Réseau interne → LAB_LAN (GREEN)

---

### SELKS (IDS/IPS)
- **OS** : Linux → Debian (64-bit)
- **RAM** : 8 Go
- **Stockage** : 50 Go
- **Adaptateurs réseau** :
  - Adaptateur 1 : Réseau interne → LAB_RED
  - Adaptateur 2 : Réseau interne → LAB_LAN

---

### Windows Server (Active Directory)
- **OS** : Windows Server 2022
- **RAM** : 4 Go minimum
- **Stockage** : 60 Go
- **Adaptateurs réseau** :
- Adaptateur 1 : Réseau interne → LAB_LAN

