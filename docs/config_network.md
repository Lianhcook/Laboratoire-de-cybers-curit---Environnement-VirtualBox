# Configuration réseau du laboratoire

Ce document décrit la configuration du réseau des différentes machines virtuelles dans le laboratoire de cybersécurité utilisant **pfSense** comme pare-feu/routeur.

---

## 1. pfSense (Pare-feu / Routeur)

| Interface | Rôle | Réseau | Type VirtualBox | Adresse IP | Passerelle | DHCP |
|-----------|------|--------|-----------------|------------|------------|------|
| em0 | WAN | Lab_Red (réseau externe) | Accès internet (NAT ou Bridge) | IP fournie par box/DHCP | fournie par box | Activé |
| em1 | LAN | Lab_LAN (réseau interne protégé) | Réseau interne → Lab_LAN | 192.168.100.1/24 | - | 192.168.100.10-192.168.100.200 |
| em2 | OPT1 (IDS/Surveillance) | Lab_IDS | Réseau interne → Lab_IDS | 192.168.200.1/24 | - | Activé ou statique |

---

## 2. Kali Linux (Attaquant)

| Interface | Réseau | Type VirtualBox | Adresse IP | Passerelle | DHCP |
|-----------|--------|-----------------|------------|------------|------|
| eth0 | Lab_Red | Réseau interne → Lab_Red | fournie par pfSense (WAN DHCP) ou statique (10.0.0.x) | IP WAN pfSense | DHCP activé |
| eth1 *(optionnel)* | NAT | NAT (pour mises à jour) | fournie par VirtualBox | VirtualBox NAT Gateway | Activé |

---

## 3. SELKS (IDS/IPS)

| Interface | Réseau | Type VirtualBox | Adresse IP | Passerelle | DHCP |
|-----------|--------|-----------------|------------|------------|------|
| eth0 | Lab_IDS | Réseau interne → Lab_IDS | 192.168.200.10/24 | 192.168.200.1 | Statique |
| eth1 | Lab_LAN | Réseau interne → Lab_LAN | 192.168.100.20/24 | 192.168.100.1 | Statique |

---

## 4. Windows Server (Cible AD)

| Interface | Réseau | Type VirtualBox | Adresse IP | Passerelle | DHCP |
|-----------|--------|-----------------|------------|------------|------|
| Ethernet0 | Lab_LAN | Réseau interne → Lab_LAN | 192.168.100.50/24 | 192.168.100.1 | Statique (recommandé) |

---

**Notes :**
- Lab_Red = réseau externe simulé (WAN pfSense)
- Lab_LAN = réseau interne sécurisé
- Lab_IDS = réseau de surveillance (IDS/IPS)
- Chaque réseau doit avoir un **plan d’adressage unique** pour éviter les conflits.
- Le DHCP est centralisé sur pfSense.
