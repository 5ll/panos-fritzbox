# IPSec VPN zwischen Palo Alto und Fritzbox inkl. mehrere Netze hinter der Palo

## Allgemein

- Es kann nicht der im Internet kommunizierte all/all/all Modus verwendet werden
- Palo möchte explizite crypto-Einstellungen

## Hilfreiche Links

https://burth-online.de/cms/pages/dokumentationen/avm-fritzbox/fritzbox---vpn---konfigurationsdatei.php
https://forum.opnsense.org/index.php?topic=9222.0


## Fritzbox Parameter erklärt

| Parameter                | Beschreibung                                                                                           |
|--------------------------|--------------------------------------------------------------------------------------------------------|
| reject_not_encrypted     | Internetzugang während VPN verbieten, kann auch die DynDNS Verbindung behinden, daher nur mit fester IP nutzen |
| dont_filter_netbios      | NetBIOS filtern, auf no gesetzt kann NetBIOS nicht genutzt werden                                      |
| mode                     | Modus der IKE-Phase1 (Agressive Mode)                                                                  |
| mode                     | Modus der IKE-Phase1 (Main Mode)                                                                       |
| phase1ss                 | Sicherheitsstrategie IKE-Phase 1, auf automatisch gesetzt                                              |
| phase2ss                 | Sicherheitsstrategie IKE-Phase 2 (IPSec)                                                               |
| accesslist               | erlaubte Netzwerke oder Hosts                                                                           |
| pppoefw                  | Router läuft im PPPOE Mode (nur als Modem)                                                             |
| dslifaces                | Router läuft im Router-Mode (NAT-Funktionalität)                                                       |
| dsldpconfig              | …                                                                                                      |
|                          |                                                                                                        |
| **Parameter für phase1ss** |                                                                                                        |
| def/3des/sha             | Zugriff auf WatchGuard Firebox                                                                         |
| alt/aes/sha              | Zugriff auf AVM Access Server                                                                          |
| def/all/all              | alle Algorithmen, DH-Gruppe default                                                                    |
| alt/all/all              | alle Algorithmen, DH-Gruppe alternativ                                                                 |
| def/all-no-aes/all       | alle Algorithmen ohne AES, DH-Gruppe default                                                           |
| alt/all-no-aes/all       | alle Algorithmen ohne AES, DH-Gruppe alternativ                                                        |
| alt/aes-3des/sha         | AES 256 Bit oder 3DES, DH-Gruppe alternativ                                                            |
| all/all/all              | alle Algorithmen, DH-Gruppe alternativ                                                                 |
|                          |                                                                                                        |
| **Parameter für phase2ss** |                                                                                                        |
| esp-aes-sha/ah-sha/comp-lzjh/pfs | Zugriff auf AVM Access Server, hohe Sicherheit                                                   |
| esp-aes-sha/ah-all/comp-lzjh-no/pfs | Zugriff auf AVM Access Server, Standardsicherheit                                              |
| esp-aes-sha/ah-no/comp-lzjh/pfs | Zugriff auf AVM Access Server, ohne AH                                                           |
| esp-3des-md5/ah-no/comp-lzjh/pfs | Zugriff auf AVM Access Server, mittlere Sicherheit                                             |
| esp-3des-sha/ah-no/comp-no/no-pfs | Zugriff auf WatchGuard Firebox                                                              |
| esp-all-all/ah-all/comp-all/pfs | alle Algorithmen, mit PFS                                                                     |
| esp-all-all/ah-all/comp-all/no-pfs | alle Algorithmen, ohne PFS                                                                  |
| esp-des\|3des-all/ah-all/comp-all/pfs | alle von Cisco unterstützten Algorithmen, mit PFS                                         |
| esp-des\|3des-all/ah-all/comp-all/no-pfs | alle von Cisco unterstützten Algorithmen, ohne PFS                                      |
| esp-des\|3des-all/ah-all/comp-no/pfs | MD5/SHA1/DES/3DES Algorithmen, mit PFS |
| esp-des|3des-all/ah-all/comp-no/no-pfs | MD5/SHA1/DES/3DES Algorithmen, ohne PFS |
| esp-3des-shal/ah-no/comp-no/pfs | Linux FreeS/WAN mit 3DES und PFS |
| esp-3des-shal/ah-no/comp-deflate/no-pfs | Linux FreeS/WAN mit 3DES ohne Kompression |
| esp-all-all/ah-none/comp-all/pfs | alle Algorithmen, ohne AH, mit PFS |
| esp-all-all/ah-none/comp-all/no-pfs | alle Algorithmen, ohne AH, ohne PFS |
| esp-aes256-3des-sha/ah-all-sha/comp-lzs-no/pfs | AES 256 Bit oder 3DES, AH optional, SHA, PFS |
| esp-aes256-3des-sha/ah-no/comp-lzs-no/pfs | AES 256 Bit oder 3DES, kein AH, SHA, PFS |
