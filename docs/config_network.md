# Configuration réseau – pfSense (3 interfaces)

## pfSense (pare‑feu/routeur)

| Interface pfSense | Rôle | Type VirtualBox | Réseau | IP/Passerelle | DHCP |
|---|---|---|---|---|---|
| **em0** | **WAN Internet** | **NAT** | NAT | IP & GW fournies par VirtualBox (10.0.2.0/24 en général) | n/a |
| **em1** | **Lab_Red** | **Réseau interne → `LAB_RED`** | 10.10.10.0/24 (exemple) | pfSense **10.10.10.1/24** (GW pour LAB_RED) | optionnel |
| **em2** | **Lab_LAN** | **Réseau interne → `LAB_LAN`** | 192.168.100.0/24 (exemple) | pfSense **192.168.100.1/24** (GW pour LAB_LAN) | **activé** (p.ex. 192.168.100.10–200) |



---

## Kali Linux (attaquant)

| NIC | Type VirtualBox | Réseau | IP suggérée | Passerelle |
|---|---|---|---|---|
| **eth0** | Réseau interne | **Lab_Red** | via DHCP pfSense ou statique **10.10.10.x/24** | **10.10.10.1** (pfSense em1) |

---

## SELKS (IDS/IPS)

| NIC | Type VirtualBox | Réseau | IP | Passerelle |
|---|---|---|---|---|
| **eth0** | Réseau interne | **Lab_LAN** | **192.168.100.20/24** | **192.168.100.1** |


---

## Windows Server (AD cible)

| NIC | Type VirtualBox | Réseau | IP | Passerelle | DNS |
|---|---|---|---|---|---|
| **Ethernet0** | Réseau interne | **Lab_LAN** | **192.168.100.50/24** | **192.168.100.1** | **192.168.100.1** (ou l’IP du DC plus tard) |

---

## Rappel câblage VirtualBox (important)

- **pfSense**
  - *Interface 1* → **NAT** (em0)
  - *Interface 2* → **Réseau interne `LAB_RED`** (em1)
  - *Interface 3* → **Réseau interne `LAB_LAN`** (em2)

- **Kali**  
  - *Interface 2* → **Réseau interne `LAB_RED`**  

- **Windows Server**  
  - *Interface 3* → **Réseau interne `LAB_LAN`**

- **SELKS**  
  - *Interface 3* → **Lab_LAN** 

---

## Ping de test
![Schéma du laboratoire](ping.png)

Depuis Kali Linux vers la passerelle LAB_LAN (192.168.2.1)
Le ping a été effectué avec succès, confirmant la connectivité entre Kali et pfSense sur le réseau Lab_IDS.

PING 192.168.2.1 (192.168.2.1) 56(84) bytes of data.
64 bytes from 192.168.2.1: icmp_seq=1 ttl=64 time=0.887 ms
64 bytes from 192.168.2.1: icmp_seq=2 ttl=64 time=1.24 ms

--- 192.168.2.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 0.887/1.065/1.244/0.178 ms


Observation :
Ce test prouve que l’interface OPT1 (Lab_IDS) de pfSense est correctement configurée et que Kali communique bien avec la passerelle.
