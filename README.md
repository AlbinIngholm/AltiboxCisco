# AltiboxCisco
En guide for hvordan man kan sette opp en Cisco Ruter mot Altibox Fiber uten å bruke hjemmesentralen

## Du trenger:

- 1x Cisco Router med IOS-XE
- 1x Bidirectional Tx1310/Rx1550 SC SFP
- UTP kabler
- USB Konsollkabel
- USB Flash Drive

## Fremgangsmåte:
**1:** Tilpass startup-config.txt til dine behov (bytt ut passord osv), og flytt den til flash driven.

**2:** Plugg flash driven inn i ruteren, og kjør følgende kommando for å overskrive eksisterende startup-config.

```
copy usbflash0:startup-config.txt flash:startup-config.txt
```

**3:** Restart ruteren

## Løsningen

Løsningen går ut på å kunne bruke fiberen rett inn i egen ruter, uten å gå gjennom hjemmesentralen.

Altibox bruker VLAN 101 for IPTV, og VLAN 102 for ren Internett-aksess.

### WAN konfigurasjon:

For å få en adresse av DHCP må vi enten spoofe mac-adressen på interfacet, eller sende DHCP options.

Interface G0/0/0 er konfigurert som følger:

```
int g0/0/0
 mac-address xxxx.xxxx.xxxx ! spoof mac på hjemmesentral
 no ip address
 no shutdown
```

Vi bruker subinterfaces for å trunke VLAN 101 og 102 over G0/0/0.

#### G0/0/0.101

```
int g0/0/0.101
 desc ** IPTV **
 encapsulation dot1q 101
 ip address dhcp
 no shutdown
```

#### G0/0/0.102
 
```
int g0/0/0.102
 desc ** Internett **
 encapsulation dot1q 102
 ip addreas dhcp
 no shutdown
```
