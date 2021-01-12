# IT2810 - Prosjekt 4

For prosjekt 4 har vi valgt å gå for alternativ A, lage en React Native klient. Applikasjonen vår er en filmdatabase som inneholder informasjon om ulike filmer hentet fra [FEND16](https://github.com/FEND16/movie-json-data?fbclid=IwAR1x59Rv0NctGe8NrlnWahhZGjgEwLFy0ZiUm_mX6ghofQVg_FJUfim-QHM). Databasen for å håndtere filmene er hosted på en virtuell maskin av NTNU.
Prosjektet er laget ved en backend som kjøres med node.js, og en frontend ved Expo og React Native. Det er lagt opp til vurdering ved å klone repoet med HTTPS.

### Setup:

- Klon repoet fra GitLab via `git clone https://gitlab.stud.idi.ntnu.no/it2810-h20/team-ad-hoc/prosjekt-4-haakon-jan.git`
- Sjekk at du er koblet til [VPN](https://innsida.ntnu.no/wiki/-/wiki/Norsk/Installere+VPN) eller [NTNU sitt nettverk](https://innsida.ntnu.no/wiki/-/wiki/Norsk/Trådløst+nett)
- Gå inn i rotmappen ved `cd prosjekt-4-haakon-jan` og kjør`npm install`
- Gå inn i backend mappen fra rotmappen ved `cd backend` og kjør`npm install`

### Kjøre backend:

- Fra backend mappen, kjør`npm start`
- Tilbakemeldingen "Server has started" skal vises i terminalen!

### Kjøre frontend:

- Lag en ny terminal i rotmappen, og kjør `npm start`
- Et browservindu skal åpne seg, og her vises metro bundleren.
- For å teste applikasjonen har du tre valg. Teste på mobil, teste i android simulator, eller teste i iOS simulator. Vi anbefaler å teste på mobil.

### Teste på mobil:

- Sørg for at mobilen er på samme nettverk som maskinen du kjører prosjektet på.
- Last ned Expo appen for enten [Android](https://play.google.com/store/apps/details?id=host.exp.exponent&hl=en_US&gl=US) eller [iPhone](https://apps.apple.com/us/app/expo-client/id982107779). Bruk en QR-leser (f.eks. kamera appen) til å scanne QR koden i Metro bundleren eller teminalen. Expo appen du lastet ned skal nå åpne seg (eventuelt trykk på forslag om å åpne den), og start testing.

---

Metro Bundler siden:

<img src="https://i.imgur.com/run5YSf.png" width=600>

---

QR kode i terminal:

<img src="https://i.imgur.com/wBMy9Ll.png" width=600>

---

Åpne applikasjon ved QR Scan
<img src="https://imgur.com/yDTEUHJ.gif" width=250>

### Teste med iOS simulator

- For å kjøre på iOS simulator må du ha [Xcode](https://apps.apple.com/us/app/xcode/id497799835?mt=12) installert på maskinen. Se expo sin egen [dokumentasjon](https://docs.expo.io/workflow/ios-simulator/) for hvordan dette gjøres.
- Trykk på "Run on iOS simulator" i metro bundleren.

### Teste med Android simulator

- For å kjøre på android simulator kan du bruke [Android Studio emulator](https://docs.expo.io/workflow/android-studio-emulator/).
- Pass på at emulatoren kjører før du trykker på "Run on Android device/emulator i metro bundleren.

## Applikasjonsbeskrivelse

### Funksjonalitet og teknologi

- Per oppgavebeskrivelse er prototypen vår laget ved React Native, og initialisert med `expo init`.
- Vi bruker redux for state management.
- Det er brukt typescript i hele prosjektet. I løsningen vår er det lagt opp til:
  - Søkemulighet ved hjelp av input felt.
  - Filtrerinsgmuligheter ved hjelp av slider, og sortering
  - Dynamisk innlasting ved en knapp i bunnen av resultatlisten.
  - Popup for å gi en mer detaljert beskrivelse av filmen
- Merk at sortering og filtrering overlapper slik at filter vil innskrenke søkemulighetene. Setter du f.eks. minimumscoren til over 5 og søker etter "Fifty Shades", vil du ikke få noen resultater.

### Bruk av tredjepartskomponenteter

- Ettersom React Native ikke kan bruke de samme bibliotekene vi brukte i prosjekt 3, har vi stort sett valgt å bruke komponenter fra [react-native-elements biblioteket](https://reactnativeelements.com).
- Dog hadde ikke React native elements noen gode løsninger på slidere med max og min verdi, så derfor hentet vi MultiSlider fra [ptomasros](https://github.com/ptomasroos/react-native-multi-slider).
- For håndtering av forskjellige lokale ip adresser, har vi brukt [Constants](https://docs.expo.io/versions/latest/sdk/constants/) for hente brukerens lokale IP addresse for fetching. Dette gjør det mulig å hente data på mobil uten å måtte gå inn i koden og manuelt sette IP adresse.

## Endringer fra prosjekt 3

- Vi har overført mye av koden fra prosjekt 3, der vi har benyttet oss av samme Redux oppsett og flere av komponentnavnene. Ettersom prosjektet vårt i innlevering 3 filtrerte og sorterte noe på backend og noe på frontend, har vi i dette prosjektet valgt å forbedre backenden slik at den er ansvarlig for all innlastning av data. Dette gjorde vi for å bevise at vi har nådd læringsmålene for dynamisk innlasting av data fra prosjekt 3.
- Ettersom vi i prosjekt 3 implementerte brukergenererte data har vi ikke fokusert på dette i prosjekt 4.
- Ved mobilapplikasjoner er innlasting av data mer kritisk med tanke på begrensede datamanegder mange har i mobilabonementet sitt. Det betyr at applikasjonen burde laste inn det den trenger for en god brukeroplevselse, men ikke noe mer. For å unngå unødvendig innlasting av data har vi lagt opp til dynamisk innlasting med 20 filmer av gangen.
- Vi har byttet ut pagiation oppsettet vårt fra prosjekt 3 med en knapp i bunnen av listevisningen som laster inn flere filmer. Dette ble gjort fordi vi synes det var et mer brukervennlig alternativ for mobil.
- Valg av filtrering og sortering skjer i samme panel ved å trykke på "Filter & Sort" knappen som ligger under søkefeltet. Vi har også laget en knapp som bytter mellom å vise resultatet i stigende eller synkende rekkefølge. Dette illustres ved ikoner som endrer seg avhengig om det er tekst eller størrelse/lengde man sorterer etter.
- Vi har også gjort en liten endring ved filtreringen, der vi isteden for å filtrere etter årstall, har valgt å filtrere etter filmens lengde.
- Vi har også valgt å gjøre flere forbedringer i valg av type, da vi i prosjekt 3 hadde noe problemer med Movie typen som ble lastet inn fra databasen, og vi brukte da any noen få steder. Vi har nå fikset dette slik at Movie typen blir korrekt.

## Styling

- Vi har valgt å lage stylesheets i bunnen av hver komponent da vi synes det er hensiktsmessig å samle styling og komponentkoden sammen da man gjerne jobber med begge deler samtidig.
- Vi har også laget en egen mappe for styling. Her ligger styling som overlapper komponenter med ulikt design for iOS og android.

## Testing

Vi har gjennomført manuelle ende til ende tester, der vi har testet at applikasjonen fungerer som den skal ved ulike brukerinteraksjoner i ulik rekkefølge.
Under har vi tenkt ut brukerhistorier som er relevante for en filmdatabase app.

### Bruk av søkefeltet

- Brukerhistorie: Som bruker ønsker jeg å finne filmer med bestemt navn.
- Hendelse: Trykk på søkefeltet og skriv inn "dark knight".
- Forventet resultat: Alle filmer med navn som har dark knight i seg vises.
- Faktisk resultat: 2 filmer med dark knight i tittelen vises.

### Bruk av filtrerting og sortering

- Brukerhistorie: Som bruker ønsker jeg å filtrere ut filmer, basert på ulike preferanser
- Hendelse: Trykk "Add filter" knapp, juster slider, sjanger og sortering og trykk "Apply filter".
- Forventet resultat: Kun filmene som inngår i kriterene av filteret blir vist.
- Faktisk resultat: Filmene som møter kriterene fra filter vises.

### Bruk av dynamisk innlasting

- Brukerhistorie: Som bruker ønsker jeg å laste inn flere filmer "on demand".
- Hendelse: Bla helt nederst i siden, trykk "Load more".
- Forventet resultat: 20 nye filmer blir lastet inn, ved å hente fra databasen.
- Faktisk resultat: 20 ny filmer blir lastet inn fra databasen.

### Bruk av popup

- Brukerhistorie: Som bruker ønsker jeg å kunne se utvidet informasjon av en film.
- Hendelse: Trykk på en film, les detaljer, trykk "Back" knapp.
- Forventet resultat: En popup skal vise utvidet informasjon fra filmen som ble trykket på. Når "Back" blir trykket på skal brukeren bli tatt tilbake til søkeresultatet.
- Faktisk resultat: En popup viser detaljer til valgt film. Ingen endringer når en går tilbake via "Back" knappen. Unntak er hvis det gjøres endringer i søkefelt, eller at ny filtering blir lagt til før brukeren trykker "Back".

### Simulasjon: Bruker ønsker å finne alle filmene som har rangering 6 til 8 i Thriller sjangeren.

- Hendelse: Trykk "Add filter", velg Thriller fra genre dropdownmenyen, dra rating slider til mellom 6 og 8.
- Forventet resultat: 5 filmer med rating rangert fra 6 til 8. Hvorav De 12 apornas armé skal være det første resultat, og Sin City skal være den siste.
- Faktisk resultat:

<img src="https://i.imgur.com/nYjEILb.png" width=300>
