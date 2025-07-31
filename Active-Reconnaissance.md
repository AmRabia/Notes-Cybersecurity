# NETWORK SCANNING TOOLS
## nmap
### scan options
| Option        | Description                                       |
|---------------|---------------------------------------------------|
| -sP ou -sn    | Ping scan (découverte d’hôtes sans scan de ports) |
| -sS           | Scan SYN (stealth scan)                           | 
| -sT           | Scan TCP connect (moins furtif)                   | 
| -sU           | Scan UDP                                          | 
| -sN, -sF, -sX | Scans furtifs sans drapeaux (bypass firewalls)    |  
| -A             | Scan agressif (OS, version, scripts, traceroute)    |   
| -O             | Détection du système d’exploitation                 |   
| -sV            | Détection de version des services                   |  
| -sC            | Exécute les scripts NSE par défaut                  |   
| --script=<nom> | Exécute un script spécifique (ex: vuln, http-title) |  
| -p <ports>      | Spécifie les ports à scanner (ex: -p 22,80,443) |  
| -F              | Scan rapide (ports les plus courants)           |  
| -r              | Ne pas randomiser l’ordre des ports             |   
| --top-ports <n> | Scanner les n ports les plus utilisés           |  
| -T<0-5>              | Vitesse du scan (0 = très lent, 5 = très rapide) |   
| --max-retries <n>    | Nombre max de tentatives par port                |  
| --min-rate <n>       | Débit minimum de paquets                         |   
| --scan-delay <temps> | Délai entre les paquets                          | 

### Common scripts NSE
Vulnerability detection:  
nmap --script vuln 192.168.1.1  
  
HTTP Enumeration:  
nmap -p 80 --script http-enum 192.168.1.1  
  
SSL/TLS Analysis:  
nmap -p 443 --script ssl-cert,ssl-enum-ciphers 192.168.1.1  

SMB Discovery:  
nmap -sV -Pn -p 445 --script smb-os-discovery 10.10.10.3

## Ping / Hping  
Ping: 
- basic networking tool
- check host reachability using ICMP Protocol

HPing: 
- advanced pen test tool
- TCP, UDP, ICP, RAW-IP protocols.
    hping3 -S -p 80 192.168.1.1 (SYN scan sur port 80)
