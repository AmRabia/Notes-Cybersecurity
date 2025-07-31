# Ports & services enumeration
## Active reconnaissance 
### nmap
Ports scan can show a Kerberos service running => Windows AD System (SMB, ...)

### Users enumeration
**Tool impacket** (collection of python classes for working with network protocols)
$ GetNPUsers.py puppy.local -no-pass -usersfile wordlist.txt -dc-ip administrator, guest, krbtgt, domain admins, root, bin, none
**Tool enum4Linux** to retrieve usernames of SMB System  
  
## Exploitation (Gaining access): privilege escalation & lateral movement
Context: I have an victim access, but he is not admin, so I will elevate my privilege to get the credentials of a victim who is admin.

### Credential harvesting
└─First thing First: check the shares I have access to
    smbmap -H TARGET-IP -u victim.name -p 'victim.pwd' -d DOMAIN -r / DEV
    smbclient //TARGET-IP/NETLOGON -U 'DOMAIN/victim.name'
    # then use `ls`, `get filename` etc.

**Tool: bloodhound**
cartographier un environnement Active Directory (AD) et identifier les chemins d’escalade de privilèges.
Identifier qui peut devenir Domain Admin, Détecter des mauvaises configurations dans AD,  Trouver des chemins d’attaque : utilisateur → admin local → délégation → DA
Visualiser les relations hiérarchiques, d’accès et de contrôle

**Exploitation techniques**
- AS REP Roasting attack: exploit kerberos authentication unsecure configuration (Authentication Server REPly: signed TGT)
- Passwords cracking: (dictionnary attack, brute force, spray, ...)
 Tool: crackmapexec, John the ripper
 crackmapexec smb TARGET-IP -u 'victime.name' -p 'pwd' --shares
- Pass the hash attack: steel the hash password and authenticate with using NTML crack
Tools: Mimikatz (be careful with IDS/EDS detection to be avoided!)
And impacket-wmi (supporting hashes authentication) or
metasploit modules (supporting hashes authentication)

Remote windows system access:
smbclient: access & interacts with SMB Shares over network
xfreerdp
evil-WinRm: remote management of windows machine ( remote command execution, ...)
net rpc (communicate with windows remote server using RPC protocol From unix-like systems. (Part of SMBA Suite)

Tools summary for pentesting Windows system:
Windows & Samba Enumeration: enum4linux
Impacket suite, psexec: execute commands on remote system
SMB Enumeration: (list shares, upload/download files, pass-the-hash, RCE, ...): smbmap
Crack password: crackmapexec, John the ripper
Windows tools: net rpc
BloodyAD


Useful powershell commands:
hostname
whoami
whoami /groups

Youtube tuto: https://www.youtube.com/watch?v=f8jGhLwCa28&t=2795s
