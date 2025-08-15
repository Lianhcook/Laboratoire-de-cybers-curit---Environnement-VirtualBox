# Configuration réseau – pfSense (3 interfaces)

## pfSense (pare‑feu/routeur)

| Interface pfSense | Rôle | Type VirtualBox | Réseau | IP/Passerelle | DHCP |
|---|---|---|---|---|---|
| **em0** | **WAN Internet** | **NAT** | NAT | IP & GW fournies par VirtualBox (10.0.2.0/24 en général) | n/a |
| **em1** | **Lab_Red** | **Réseau interne → `Lab_Red`** | 10.10.10.0/24 (exemple) | pfSense **10.10.10.1/24** (GW pour Lab_Red) | optionnel |
| **em2** | **Lab_LAN** | **Réseau interne → `Lab_LAN`** | 192.168.100.0/24 (exemple) | pfSense **192.168.100.1/24** (GW pour Lab_LAN) | **activé** (p.ex. 192.168.100.10–200) |

> Adapte les plages si tu en utilises d’autres, mais **chaque réseau doit être unique**.

---

## Kali Linux (attaquant)

| NIC | Type VirtualBox | Réseau | IP suggérée | Passerelle |
|---|---|---|---|---|
| **eth0** | Réseau interne | **Lab_Red** | via DHCP pfSense ou statique **10.10.10.x/24** | **10.10.10.1** (pfSense em1) |
| **eth1 (optionnel)** | NAT | NAT (mises à jour) | auto | 10.0.2.2 (gateway NAT VB) |

---

## SELKS (IDS/IPS)

| NIC | Type VirtualBox | Réseau | IP | Passerelle |
|---|---|---|---|---|
| **eth0** | Réseau interne | **Lab_LAN** | **192.168.100.20/24** | **192.168.100.1** |
| **eth1 (optionnel)** | Réseau interne | **Lab_Red** | **10.10.10.20/24** | **10.10.10.1** |

*(Tu peux n’en mettre qu’un si tu préfères placer l’IDS côté LAN seulement.)*

---

## Windows Server (AD cible)

| NIC | Type VirtualBox | Réseau | IP | Passerelle | DNS |
|---|---|---|---|---|---|
| **Ethernet0** | Réseau interne | **Lab_LAN** | **192.168.100.50/24** | **192.168.100.1** | **192.168.100.1** (ou l’IP du DC plus tard) |

---

## Rappel câblage VirtualBox (important)

- **pfSense**
  - *Adaptateur 1* → **NAT** (em0)
  - *Adaptateur 2* → **Réseau interne `Lab_Red`** (em1)
  - *Adaptateur 3* → **Réseau interne `Lab_LAN`** (em2)

- **Kali**  
  - *Adaptateur 1* → **Réseau interne `Lab_Red`**  
  - *(Optionnel) Adaptateur 2 → NAT* pour apt update

- **Windows Server**  
  - *Adaptateur 1* → **Réseau interne `Lab_LAN`**

- **SELKS**  
  - *Adaptateur 1* → **Lab_LAN** (ou Lab_Red selon ton choix IDS)

---

## Routes & ping de test

- Depuis **Kali** : `ping 10.10.10.1` (GW pfSense em1) puis un hôte du LAN si règle autorisée.  
- Depuis **Windows** : `ping 192.168.100.1` (GW pfSense em2).  
- Accès GUI pfSense :  
  - côté LAN : `https://192.168.100.1`  
  - côté Lab_Red (si autorisé) : `https://10.10.10.1`
