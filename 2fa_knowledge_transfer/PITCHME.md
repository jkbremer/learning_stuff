---?color=linear-gradient(180deg, #1E5C97 75%, black 25%)
## Zwei-Faktor Authentifizierung
@snap[south span-100]
Julia Bremer
Univention GMBH
@snapend

---
## **Agenda**

@snap[west-south span-100]
@ol[list-spaced-bullets text-06](true)
- Das Problem mit Passwörtern
- Warum 2FA?
- TOTP/HOTP
- Authenticator Apps
- Biometrische Daten
- Security Keys
- Vergleich der Faktoren
- FIDO2 und WebAuthN
@olend
@snapend

@snap[east span-60]
@img[shadow](assets/img/mfa.jpg)
@snapend
---
## MFA & 2FA
@snap[west-south span-60]
@ol[list-spaced-bullets text-07](true)
- **MFA**: Mehr als ein Faktoren zur Authentifizierung
- **2FA**: Genau zwei Faktoren
- **Beispiel**: Bankkarte + PIN
- Man unterscheidet in drei Kategorien
- **Besitz** (z.B. Smartcard)
- **Inhärenz** (z.B. Fingerabdruck)
- **Wissen** (z.B. Passwort)
@snapend
@snap[south-east span-40]
@img[shadow](assets/img/2fa.jpg)
@snapend


---
## **Warum 2FA?**
@snap[west-south span-50]
@ol[list-spaced-bullets text-06](true)
- Passwörter sind **unbequem**
- Passwörter werden **wiederverwendet**
- Passwörter werden **dokumentiert**
- Passwörter werden **vergessen**
- Passwörter werden **gestohlen**
- Passwörter werden **gefished**
- 43% Erfolgsrate bei guten **Phishing-Seiten**
- Beliebteste Passwörter 2020: **123456, 12345678, password**
@olend
@snapend
@snap[east span-50]
@img[shadow](assets/img/fish.png)
@snapend

---
## **Das Passwort-Problem**
##### Auch **komplexe Passwörter** helfen gegen die meisten Angriffsvektoren nicht:
@snap[south-west span-80 text-06]
@table[Does your Password matter?](assets/tables/pdm1.csv)
@snapend
---
## **OTP: One Time Passwords**

@snap[west-south span-70]
@ol[list-spaced-bullets text-06](true)
- **T**ime based **OTP**
- **TOTP** ist eine **Erweiterung von HOTP**
- Die meisten Arten von 2fa nutzen **TOTP**
- verwendet **symmetrische** Verschlüsselung
- geheimer Schlüssel wird mit einem Zeitintervall zusammen **gehasht**
- Früher meist mithilfe eines Hardware-Authenticator
- Ein Hardware-Authenticator pro Service notwendig
- Schlüssel muss **im Klartext beim Service** liegen
@olend
@snapend
@snap[north-east span-30]
@img[shadow](assets/img/hotp.png)
@snapend

@snap[east span-30 text-07]
@math
`\[C_t= \frac{t-t_0}{t_x}\]`
`\[TOTP_k = HMAC(k, C_t)\]`
@mathend
@snapend

---
## **Authenticator Apps**

@snap[west-south span-60]
@ol[list-spaced-bullets text-08](true)
- Verwenden ebenfalls **TOTP**
- Können auf jedem **Smartphone** laufen
- Uhren müssen **synchron** sein
- **Komfortabel**, da die meisten ein Smartphone haben
- Setup meist durch **QR-Code**, um der App den Schlüssel zu übertragen
@olend
@snapend
@snap[south-east span-40]
@img[shadow](assets/img/googlauth.jpg)
@snapend

---?image=assets/img/fingerprint.jpg&opacity=100&position=right&size=50%
## **Biometrische Daten**

@snap[west-south span-80]
@ol[list-spaced-bullets text-06](true)
- Authentifikation mithilfe **inherenter Biomarkern**
- z.B. Gesicht, Stimme, Iris, Fingerabdruck
- Beispiel: **Windows hello**
- Meist (aus Sicherheitsgründen) nur **lokale Authentifizierung** angeboten
- Bild der Biometrie wird gemacht, abstrahiert und verglichen mit den vorliegenden Daten
- **Ähnlichkeit** wird verglichen
- Hohe **Fehlerrate**
- Leicht zu **fälschen**
@olend
@snapend

---
## **Microsoft & Windows Hello**

@snap[west-south span-100]
@ol[list-spaced-bullets text-08](true)
- Login per **Biometrie**, Gesichtserkennung
- Auf **einen lokalen Rechner** beschränkt
- Seit 2019 unterstützt Microsoft auch **FIDO2** per Security Key
- Hierbei funktioniert die Authentifikation gegen AD/Azure
- Lokaler Service holt sich nach FIDO-Auth ein TGT im Namen des Users
@olend
@snapend

---
## **Security Keys**

@snap[west-south span-70]
@ol[list-spaced-bullets text-06](true)
- USB-Token (bluetooth, nfc ebenfalls möglich)
- Key storage devices
- verwenden **asymmetrische Verschlüsselung**
- Vor Verwendung muss ein Key **registriert** werden
- Dabei wird ein **neues Schlüsselpaar erzeugt**
- **Mehrere Schlüssel** pro Karte/Token speicherbar
- Token oftmals **selbst durch PIN/Biometrie gesichert**
@olend
@snapend
@snap[north-east span-20]
@img[shadow](assets/img/yubikey.png)
@snapend

---
## **Vergleich**
@snap[south span-100]
@ol[list-spaced-bullets text-08](true)
@olend
@snapend
@snap[west span-100 text-07]
@table[Does your Password matter?](assets/tables/cred-secure.csv)
@snapend

---
## FIDO2
@snap[west-south span-70]
@ol[list-spaced-bullets text-06](true)
- FIDO-Protokolle erstellt von der **FIDO-Allianz** (Google, Paypal, RSA, Amazon, Facebook, Visa, Samsung, Apple....)
- FIDO =**F**ast **ID**entitiy **O**nline
- Ziel: **Offene Standards** definieren
- verwendet **asymmetrische Verschlüsselung**
- Ein Authenticator für viele Services
- Alle Smartphones ab **Android 7** sind selbst Security Keys für FIDO2
- Muss durch **Nutzeraktion** aktiviert werden (Drücken des Buttons)
- generiert bei **Registrierung** ein neues Schlüsselpaar
@olend
@snapend
@snap[east span-40]
@img[shadow](assets/img/webauthn-logo.png)
@snapend
---
## **FIDO2**
@snap[west-south span-100 text-06]
@ol[list-spaced-bullets](true)
- Besteht aus **CTAP**(FIDO-Allianz) und **WebAuthn**(W3C)
- Authenticator generiert bei Registrierung ein **neues Schlüsselpaar**
- verwendet RSA/ECDSA P-256 (Elliptic Curve Digital Signature Algorithm)
- Server schickt Challenge an Authenticator zum verifizieren
- Authenticator schickt Signatur der Challenge
- Testbar auf https://webauthn.io/ und https://webauthn.me/
@olend
@snapend
@snap[south span-60]
@img[shadow](assets/img/fido2.png)
@snapend
---
## FIDO2
@snap[west-south span-100 text-08]
@ol[list-spaced-bullets](true)
1. Service und Web-application kommunizieren per WebAuthn-API mit dem Browser
1. Browser kommunziert per CTAP mit dem Token
1. Service erzeugt zufällige Challenge
1. Token signiert Challenge
1. Private Key wird bei Registrierung abhängig von der **ClientID** 
@olend
@snapend

---?image=assets/img/fido2-register.png&opacity=100&position=bottom&size=100% 85%
### **FIDO2 - Registrierung**
---?image=assets/img/fido2-auth.png&opacity=100&position=center&size=100% 75%
### **FIDO2 - Authentifizierung**

---
## FIDO2 - Vulnerabilities
@snap[west-south span-100 text-05]
## Anfälligkeit für häufige Angriffsvektoren:
@ol[list-spaced-bullets](true)
- **Phishing: Nein** der Schlüssel speichert eine Relying Party ID (domainname), weicht diese ab kann keine Authentifizierung statt finden
- **Replay Attack: Nein** aufgrund der zufällig generierten Challenge
- **Key-Logger: Nein** es muss nichts eingetippt werden
- **Data Breach: Nein** es wird lediglich ein Public Key gespeichert
@olend
## Mögliche Angriffsvektoren:
@ol[list-spaced-bullets](true)
- Über **Diebstahl** des Keys
- Über **unsichere Account Reaktivierung**: Bei Verlust fällt der Anbieter auf Passwort-Authentifizierung zurück
@olend
@snapend


---
#### Gute Quellen(1)

@snap[west-south span-100]
@ol[list-spaced-bullets text-06](false)
- William Brown (SUSE) https://samba.plus/blog/detail/sambaxp-2020-retrospective-the-psychology-of-multifactor-authentication-william-brown
- Google MasterClass- WebAuthn and Security Keys: https://identiverse.gallery.video/detail/video/6159111760001/6-26-google-masterclass--webauthn-and-security-keys...-_-identiverse-2018?autoStart=true&q=fido
- WebAuthN specs: https://www.w3.org/TR/webauthn-1
- https://sar.informatik.hu-berlin.de/research/publications/SAR-PR-2020-04/SAR-PR-2020-04_.pdf
- Breaking FIDO2 (Blackhat Con): https://www.youtube.com/watch?v=J53Ya7E5HGQ&t=29s
- Moderne Verfahren der Kryptographie, Albrecht Beutelspacher, Springer Verlag
@olend
@snapend
---
#### Gute Quellen(2)

@snap[west-south span-100]
@ol[list-spaced-bullets text-06](false)
- FIDO2, WebAuthn und CTAP. Wie gelingt Authentisieren ohne Passwörter?, Marc Kasberger, Studienarbeit
- CTAP specs: https://fidoalliance.org/specs/fido-v2.0-ps-20190130/fido-client-to-authenticator-protocol-v2.0-ps-20190130.pdf
- Phishing as a Science: https://www.youtube.com/watch?v=Z20XNp-luNA
- https://techcommunity.microsoft.com/t5/azure-active-directory-identity/your-pa-word-doesn-t-matter/ba-p/731984
- https://techcommunity.microsoft.com/t5/itops-talk-blog/ops108-windows-authentication-internals-in-a-hybrid-world/ba-p/2109557?WT.mc_id=ModInfra-12977-rclaus
- Build your first WebAuthn App (Google): https://codelabs.developers.google.com/codelabs/webauthn-reauth#0
- WebAuthn 101 - Demystifying WebAuthn (Blackhat Con): https://www.youtube.com/watch?v=RFACQvL_8S4
@olend
@snapend
---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%
## **Danke** für eure Aufmerksamkeit

---?color=linear-gradient(#1E5C97 15%, white 85%)
## Extras (Attestation)
@img[shadow](assets/img/fido-attestation-structures.svg)
