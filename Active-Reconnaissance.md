# NETWORK SCANNING
## nmap
### Basic scan
Option	Description
-sP ou -sn	Ping scan (découverte d’hôtes sans scan de ports)
-sS	Scan SYN (stealth scan)
-sT	Scan TCP connect (moins furtif)
-sU	Scan UDP
-sN, -sF, -sX	Scans furtifs sans drapeaux (bypass firewalls)


### Advanced scan
-A	Scan agressif (OS, version, scripts, traceroute)
-O	Détection du système d’exploitation
-sV	Détection de version des services
-sC	Exécute les scripts NSE par défaut
--script=<nom>	Exécute un script spécifique (ex: vuln, http-title)

### Target scan
-p <ports>	Spécifie les ports à scanner (ex: -p 22,80,443)
-F	Scan rapide (ports les plus courants)
-r	Ne pas randomiser l’ordre des ports
--top-ports <n>	Scanner les n ports les plus utilisés

### Furtive scan
-T<0-5>	Vitesse du scan (0 = très lent, 5 = très rapide)
--max-retries <n>	Nombre max de tentatives par port
--min-rate <n>	Débit minimum de paquets
--scan-delay <temps>	Délai entre les paquets
