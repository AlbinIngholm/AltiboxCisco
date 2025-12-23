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