# Configuration réseau – pfSense (3 interfaces)

## pfSense (pare‑feu/routeur)

| Interface pfSense | Rôle | Type VirtualBox | Réseau | IP/Passerelle | DHCP |
|---|---|---|---|---|---|
| **em0** | **WAN Internet** | **NAT** | NAT | IP & GW fournies par VirtualBox (10.0.2.15/24) | n/a |
| **em1** | **Lab_Red** | **Réseau interne → `LAB_RED`** | 192.168.1.1/24 | pfSense **192.168.1.1/24** (GW pour LAB_RED) | **activé** ( 192.168.1.100–199 ) |
| **em2** | **Lab_LAN** | **Réseau interne → `LAB_LAN`** | 192.168.2.1/24  | pfSense **192.168.2.1/24** (GW pour LAB_LAN) | **activé** ( 192.168.2.100–199 ) |



---

## Kali Linux (attaquant)

| NIC | Type VirtualBox | Réseau | IP | Passerelle |
|---|---|---|---|---|
| **eth0** | Réseau interne | **Lab_Red** |  **192.168.1.100/24** | **192.168.1.1** (pfSense em1) |

---

## SELKS (IDS/IPS)

| NIC | Type VirtualBox | Réseau | IP | Passerelle |
|---|---|---|---|---|
| **eth0** | Réseau interne | **Lab_LAN** | **192.168.2.102/24** | **192.168.2.1** |


---

## Windows Server (AD cible)

| NIC | Type VirtualBox | Réseau | IP | Passerelle | DNS |
|---|---|---|---|---|---|
| **Ethernet0** | Réseau interne | **Lab_LAN** | **192.168.2.101/24** | **192.168.2.1** | **192.168.2.1** |


---

## Ping de test
![Schéma du laboratoire](ping.png)

Depuis Kali Linux vers la passerelle LAB_LAN (192.168.2.1)
Le ping a été effectué avec succès, confirmant la connectivité entre Kali et pfSense sur le réseau Lab_IDS.

Observation :
Ce test prouve que l’interface OPT1 (LAB_LAN) de pfSense est correctement configurée et que Kali communique bien avec la passerelle, pareille avec les utilisateurs du reseau LAB_RED.
