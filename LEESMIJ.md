# Constructif Gereedmelding CV – installeren op GitHub + Firebase

Eenmalig ongeveer 15 minuten werk. Daarna loggen de jongens in met de **monteurscode** en jij met de **kantoorcode**.

## 1. Firebase-project aanmaken
1. Ga naar https://console.firebase.google.com en log in met je Google-account.
2. **Project toevoegen** → naam bijv. `gereedmelding-cv` → Google Analytics mag uit → **Project maken**.

## 2. Inloggen met codes instellen
1. Menu links: **Build → Authentication → Aan de slag**.
2. Tab **Sign-in method** → **E-mail/wachtwoord** → inschakelen → Opslaan.
3. Tab **Users** → **Gebruiker toevoegen**, twee keer:
   - E-mail `kantoor@gereedmelding.app` – wachtwoord = jouw **kantoorcode**
   - E-mail `monteur@gereedmelding.app` – wachtwoord = de **monteurscode**
   - Codes minimaal 6 tekens. Gebruik iets wat niet makkelijk te raden is.
4. Tab **Settings → Authorized domains → Domein toevoegen**: `JOUWNAAM.github.io` (je GitHub-gebruikersnaam).

## 3. Database aanmaken
1. Menu links: **Build → Firestore Database → Database maken**.
2. Locatie: **europe-west4 (Nederland)** → **productiemodus** → Maken.
3. Tab **Regels** (Rules): vervang alles door de inhoud van `firestore.rules` → **Publiceren**.

## 4. App koppelen aan Firebase
1. Tandwiel links boven → **Projectinstellingen** → onderaan **Je apps** → het icoon **`</>`** (web).
2. Bijnaam bijv. `gereedmelding` → **App registreren** (Firebase Hosting niet nodig).
3. Kopieer de waarden uit `firebaseConfig` (apiKey, authDomain, projectId, …) naar **`firebase-config.js`** op de plekken met `VUL-IN`.

## 5. Op GitHub zetten
1. Op github.com: **New repository** → naam bijv. `gereedmelding` → Public → Create.
2. **Add file → Upload files** → sleep alle bestanden uit deze map erin (index.html, firebase-config.js, firestore.rules, manifest.webmanifest, icon-512.png, LEESMIJ.md) → Commit.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch **main** / **(root)** → Save.
4. Na een minuutje staat de app op: `https://JOUWNAAM.github.io/gereedmelding/`

## 6. Gegevens overzetten uit de claude.ai-versie
1. Open de oude app in claude.ai → **Opgeslagen meldingen → ⬇ Back-up maken**.
2. Open de nieuwe app, log in met de **kantoorcode** → **Opgeslagen meldingen → ⬆ Back-up terugzetten** → kies het bestand.
   Meldingen, foto's, complexen en gevelfoto's komen mee. De standaard radiatoren stel je opnieuw in.

## 7. De jongens
- Stuur ze de link en de monteurscode. Ze blijven ingelogd op hun telefoon.
- Tip: in Safari/Chrome **Deel → Zet op beginscherm**, dan werkt het als een app.
- Werkt ook zonder bereik: wat ze invullen wordt bewaard en verstuurd zodra er weer verbinding is (inloggen zelf moet wel online).

## Wie mag wat
| | Monteur | Kantoor |
|---|---|---|
| Woning kiezen, invullen, foto's, handtekening, Woning gereed, PDF van de woning | ✓ | ✓ |
| Complex inlezen, los nummer, invul-Excel, woonlagen | – | ✓ |
| Gevelfoto uploaden en nummers plaatsen | – | ✓ |
| Standaard radiatoren | – | ✓ |
| Alles downloaden (ZIP), Excel-overzicht, gevel-PDF, back-up | – | ✓ |
| Meldingen verwijderen | – | ✓ |

Dit wordt afgedwongen door de Firestore-regels, niet alleen verborgen in het scherm.

## Code wijzigen
Firebase → Authentication → Users → bij de gebruiker **⋮ → Gebruiker verwijderen** en opnieuw toevoegen met dezelfde e-mail en de nieuwe code. Iedereen moet daarna opnieuw inloggen.

## Kosten
Het gratis Firebase-plan (Spark) is ruim genoeg: 1 GB opslag (≈ 240 woningen met elk 6 foto's is ca. 300 MB), 50.000 keer lezen en 20.000 keer schrijven per dag.
