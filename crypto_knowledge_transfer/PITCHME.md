---?color=linear-gradient(180deg, #1E5C97 75%, black 25%)
# Kryptografie
@snap[south span-100]
Johanna Quednau - Julia Bremer
@snapend

---
### **Agenda**

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Kryptografie
- Obfuscation / Hashing / Encryption
- Block cipher / Stream cipher
- **Symmetrische** Verschlüsselung
- **Asymmetrische** Verschlüsselung
- Signaturen
- Zertifikate
@olend
@snapend

@snap[east span-50]
@img[shadow](assets/img/keys.jpg)
@snapend
---

### Kryptografie

Die Wissenschaft der **Verschlüsselung**
@snap[south span-100]
@img[shadow](assets/img/crypt_gebiete.png)
@snapend

---
### Obfuscation

@snap[west-south span-100]
@ol[list-spaced-bullets text-08](false)
- **Security by Obscurity**
- Bei Obfuscation geht es nur darum Dinge **unverständlicher** zu machen
- Für Computer leicht drüber hinwegzusehen, für Menschen schwer
- Keine gute Sicherheitsmaßnahme
- Beispiel: AD supplementalCredentials werden obfuscated übertragen, damit in network traces nicht klar erkennbar ist, dass es Credentials sind.
@olend
@snapend

---
### Hash

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Im Gegensatz zur Verschlüsselung eine mathematische **Einwegsfunktion**
    - Das heißt, man kann aus einem Hash **nicht** die originalen Daten rekonstruieren
- Verwendungszweck meist in Kombination mit Verschlüsselung
- Problem: Wurde ein Passwort zu einem Passworthash ermittelt, sind dann alle aufgeflogen die dieses Passwort verwenden?
- **Rainbowtables** mappen Worte zu Hashes, die häufigsten sind also bekannt
- Damit diese Rainbowtables nicht funktionieren **saltet** man
- Hashfunktionen können **Kollisionen** haben
- Kollision heißt es exisieren mehrere Wörter, die den gleichen Hash erzeugen
@olend
@snapend

---
### Salt

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Ein Extrawort, dass dem Passwort vor dem Hashing hinzugefügt wird.
- Dabei ist es nicht wichtig, dass der Salt geheim ist, nur dass er bei **jedem Benutzer unterschiedlich** ist.
- Durch die Zuführung eines Saltes, kann man den Hash nicht mehr in Rainbowtables nachsehen.
- Und gleiche Passwörter anhand der Gleichheit des Hashes erkennen.
- Beispiel: Bei Kerberos ist der default salt **username@DOMAINNAME**
- krb5key =  Salt + Hashfunktion(Salt+Pwd)
@olend
@snapend

---
### Encryption

@snap[west-south span-100]
@ol[list-spaced-bullets text-08](false)
- Der eigentliche Fokus der Kryptografie
- Eine **umkehrbare** Funktion, bei der es eine Funktion **e**(ncryption) und eine Funktion **d**(ecryption) gibt.
- Zwei grundlegende Operationen um starke Verschlüsselung zu erreichen sind **Konfusion** und **Diffusion**
- **Konfusion**: Verschleierung von Zusammenhang von Schlüssel und Chiffre
- **Diffusion**: Verschleierung von statistischen Eigenschaften des Klartextes
@olend
@snapend

---
### **Symmetrische** Verschlüsselung

@snap[west-south span-100]
@ol[list-spaced-bullets text-08](false)
- In der symmetrischen Verschlüsselung kann mit **dem selben Schlüssel ver- und entschlüsselt** werden
- Beide Teilnehmer müssen im Besitz dieses Schlüssels sein
- Die Verteilung des Schlüssels ist ein Hauptproblem beim symmetrischen Verfahren
- Darum verwendet man auch **hybride** Verfahren, bei denen der Schlüsselaustausch asymmetrisch vollstreckt wird
- Man teilt die symmetrischen Verfahren in **Blockchiffren** und **Stromchiffren** auf
@olend
@snapend

---
### Stream vs Block Cipher
@snap[west-south span-100]
@ol[list-spaced-bullets text-08](false)
- Bei der Stromchiffre wird **jeder Klartextbit einzeln** verschlüsselt
   - Es gibt keinen (automatischen) Integritätsschutz
   - Beispiel: **RC4**
- Bei der Blockchiffre wird immer ein ganzer **Block Klartextbits gleichzeitg** verschlüsselt
   - Die statistischen Eigenschaften bleiben im Chiffrat erhalten
   - Beispiel: **DES**, **AES**
   - meistens werden Blockchiffren genutzt
@olend
@snapend

---
### Asymmetrische Verschlüsselung
#### **Public-Key-Kryptografie**

@snap[west-south span-100]
@ol[list-spaced-bullets text-06](false)
- Hier gibt es **zwei verschiedene** Schlüssel, einen **verschlüsselnden** und einen **entschlüsselnden**
- Diese Schlüssel werden auch **public key** und **private key** genannt
- Der public key **muss nicht geheim gehalten** werden
- Diese Verschlüsselungsalgorithmen basieren darauf, dass es Prinzipien gibt, die für Computer leicht zu errechnen sind, deren Inverse allerdings sehr schwer zu berrechnen ist.
- Man nennt dies auch **Einwegsfunktionen** die im Grunde **injektive** Abbildungen sind
- Wird oft nur für **Signaturen** und zum **Schlüsselaustausch** verwendet
@olend
@snapend

---
### Asymmetrisch vs Symmetrische Verschlüsselung

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Hauptproblem der symmetrischen Verschlüsselung ist das **Schlüsselaustauschproblem**
- Nur mit asymmetrischen Keys kann **signiert** werden
- Asymmetrische Keys müssen **sehr lang** sein um ähnlich sicher wie symmetrische Keys zu sein
- Symmetrische Verschlüsselung ist sehr **schnell und effizient**
@olend
@snapend

---
### Signaturen

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Soll **Zurechenbarkeit** und **Nichtabstreitbarkeit** erreichen, ähnlich eine gewöhnlichen Signatur
- Kann nur durch asymmetrische Verschlüsselung zustande kommen
- Dabei geht es **nicht um Verschlüsselung** der Nachricht. Nachrichten können signiert sein, ohne verschlüsselt zu sein
- **RSA-Signatur** wird häufig verwendet und basiert auf **RSA-Verschlüsselung**
@olend
@snapend
---
### Zertifikate

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Ist ein Public Key und verweist darauf
- Wird von einer **CA - Certificate Authority** "beglaubigt" also einer **trusted third party**
- Vertrauen der CA ist erforderlich um Sicherheit herzustellen
- Der Standart ist **X.509v3** und wird auch für **HTTPS** verwendet
- **HTTPS** steht für **HTTP over SSL bzw. neuer TLS** und verschlüsselt Web-Nachrichten mithilfer solcher Zertifikate
- Bei **HTTP** hingegen werden Nachrichten im Klartext ausgetauscht 
@olend
@snapend

---
#### Gute Quellen

@snap[west-south span-100]
@ol[list-spaced-bullets text-07](false)
- Einführung in DES: https://www.youtube.com/watch?v=H7bvLU-2JUI
- Buch Kryptografie verständlich
- Kapitel IT-Sicherheit aus "Betriebssysteme" von Tanenbaum
@olend
@snapend
---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%
## **Danke** für eure Aufmerksamkeit
