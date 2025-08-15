Configuration réseau du laboratoire

Ce document décrit la configuration du réseau des différentes machines virtuelles dans le laboratoire de cybersécurité utilisant pfSense comme pare-feu/routeur.

1. pfSense (Pare-feu / Routeur)
Interface	Rôle	Réseau	Tapez VirtualBox	Adresse IP	Passerelle	DHCP
em0	BLÊME	Lab_Red (réseau externe)	Adaptateur réseau → Accès internet (NAT ou Bridge)	IP fournie par box/DHCP	fourni par boîte	Actif
em1	réseau local	Lab_LAN (réseau interne protégé)	Réseau interne →Lab_LAN	192.168.100.1/24	-	Actif (192.168.100.10-192.168.100.200)
em2	OPT1	Réseau de surveillance / IDS (SELKS)	Réseau interne →Lab_IDS	192.168.200.1/24	-	Actif ou statique
2. Kali Linux (Attaquant)
Interface	Réseau	Tapez VirtualBox	Adresse IP	Passerelle	DHCP
eth0	Lab_Red	Réseau interne →Lab_Red	fourni par pfSense (WAN DHCP) ou statique (10.0.0.x)	IP WAN pfSense	DHCP activé
eth1(facultatif)	NAT	Accès internet direct (pour mises à jour)	fourni par VirtualBox	Passerelle NAT VirtualBox	Actif
3. SELKS (IDS/IPS)
Interface	Réseau	Tapez VirtualBox	Adresse IP	Passerelle	DHCP
eth0	Lab_IDS	Réseau interne →Lab_IDS	192.168.200.10/24	192.168.200.1 (pfSense OPT1)	Statique
eth1	Lab_LAN	Réseau interne →Lab_LAN	192.168.100.20/24	192.168.100.1	Statique
4. Serveur Windows (Cible AD)
Interface	Réseau	Tapez VirtualBox	Adresse IP	Passerelle	DHCP
Ethernet0	Lab_LAN	Réseau interne →Lab_LAN	192.168.100.50/24	192.168.100.1 (réseau local pfSense)	Statique (recommandé)
