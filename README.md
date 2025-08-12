# Laboratoire de cybersécurité - Environnement VirtualBox

## Description
Ce projet met en place un laboratoire de cybersécurité virtuelle permettant de simuler des attaques et d'analyser le trafic réseau.  
L'environnement repose sur VirtualBox et intègre plusieurs machines virtuelles représentant différents rôles réseau : **attaquant**, **pare-feu**, **IDS/IPS** et **cible Active Directory**.

---

## Architecture du Lab

| Machine        | Rôle                       | Système d'exploitation / Logiciel | Réseau(x)              |
|----------------|---------------------------|------------------------------------|------------------------|
| Kali Linux     | Attaquant                  | Kali Linux 2025.2                 | LAB_RED, NAT           |
| IPFire         | Pare-feu / Routeur         | IPFire                             | LAB_RED, LAB_LAN       |
| SELKS          | IDS/IPS                    | SELKS 10                           | LAB_RED, LAB_LAN       |
| Windows Server | Cible AD / Services        | Windows Server 2022                | LAB_LAN                |

## Schéma du réseau

![Schéma du laboratoire](images/schema.png)

---

## Réseaux

- **LAB_RED** → Réseau externe simulé (attaquant vers pare-feu)  
- **LAB_LAN** → Réseau interne protégé (machines internes)  
- **NAT** *(optionnel)* → Permet les mises à jour des outils depuis Internet  

---

## Installation

### 1. Prérequis
- VirtualBox + Pack d'extension
- Images ISO :
  - Kali Linux 2025.2
  - Dernière version d'IPFire
  - SELKS 10 (avec ou sans bureau)
  - Windows Server 2022 (ou 2019)

### 2. Configuration réseau dans VirtualBox

#### IPFire
- Adaptateur 1 : Réseau interne → `LAB_RED`
- Adaptateur 2 : Réseau interne → `LAB_LAN`

#### Kali Linux
- Adaptateur 1 : Réseau interne → `LAB_RED`
- Adaptateur 2 : NAT *(optionnel)*

#### SELKS
- Adaptateur 1 : Réseau interne → `LAB_RED`
- Adaptateur 2 : Réseau interne → `LAB_LAN`

#### Windows Server
- Adaptateur 1 : Réseau interne → `LAB_LAN`

---

## Objectifs pédagogiques
- Simuler des attaques et tester des règles de pare-feu  
- Observer le trafic réseau avec SELKS (Suricata, Kibana, etc.)  
- Mettre en place un Active Directory sur Windows Server  
- Développer des compétences en cybersécurité offensive et défensive  

---

## Licence
Projet libre pour un usage éducatif et non commercial.

