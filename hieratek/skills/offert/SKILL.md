---
name: offert
description: Ta fram en offert för ett jobb hos företaget som är anslutet till Hieratek, från ärende och kalkyl till godkänd slutlig offert, PDF och kundens svar. Använd när användaren vill räkna, skriva, skicka eller följa upp en offert, ett pris eller ett anbud på ett jobb.
---

# Offert

Arbeta alltid mot företagets sparade uppgifter hos Hieratek. Kalkylen räknas
av Hierateks verktyg; räkna aldrig fram priset själv.

## Före första steget

1. Anropa `workspace_status`. Säg vilket företag du arbetar i, med namnet ur
   svaret: "Jag arbetar i Exempel Måleri AB." Är företaget fel eller
   okänt: stanna och be användaren ansluta rätt konto.
2. Hitta jobbet med `case_list`, eller skapa ett nytt med `case_create` om
   användaren bekräftar att det är ett nytt jobb. Läs det med `case_get`.

## Prislista

3. Läs företagets prislista med `price_list_get`. Behandlingarnas namn är
   de enda behandlingar kalkylen kan räkna med.
   - Har ägaren en egen prislista, gamla offerter eller kalkyler: följ
     `prisimport` och läs in värdena därifrån.
   - Saknas prislista: fråga ägaren samlat om timkostnad, påslag, moms och
     varje behandling med färgåtgång, förarbete, tid per strykning och
     materialpris. Föreslå den med `price_list_propose` och ge ägaren länken.
     Ingen kalkyl kan göras förrän ägaren har godkänt den på sidan.
   - Vill ägaren ändra ett pris: läs listan, ändra bara det ägaren sagt och
     föreslå hela listan med `price_list_propose`. Ge ägaren länken; den nya
     listan gäller först när ägaren godkänt den på sidan.
   - Hitta aldrig på värden och använd aldrig en annan firmas priser.
   - Ge varje behandling ett display_name med ägarens egna ord, så som
     kunden ska läsa det i offerten, till exempel "Väggmålning, två
     strykningar". Saknas namnet står behandlingens nyckel i offerten.

## Offertprofil

Offertprofilen är företagets egna uppgifter i varje offert. Läs den med
`quote_profile_get` före första offerten.

- Saknas profil: fråga ägaren samlat om företagsnamn, organisationsnummer,
  adress, telefon, e-post, om företaget är godkänt för F-skatt,
  betalningsvillkor, hur många dagar offerten gäller, kontaktperson och
  ägarens egen text om villkor och förbehåll. Föreslå profilen med
  `quote_profile_propose` och ge ägaren länken. Den gäller först när ägaren
  har godkänt den på sidan.
- Skriv aldrig villkor, betalningsvillkor eller förbehåll åt ägaren, och
  föreslå inga formuleringar. Vill ägaren inte ha någon text: lämna fältet
  tomt, så visas inget i offerten.
- En ändring går samma väg: läs profilen, ändra bara det ägaren sagt och
  föreslå hela profilen igen.

### Egen offertmall

Ägaren kan ladda upp sin egen offertmall (Word, PDF eller bild) i chatten.

1. Spara filen i företagets egen Drive med användarens egen Drive-koppling.
2. Räkna filens SHA-256 med ditt kodverktyg.
3. Föreslå profilen med `quote_profile_propose` med mallen i template:
   filens id, SHA-256, format (docx, pdf, png eller jpeg) och filnamn. Ägaren
   godkänner mallen som en del av profilen.

Saknas Drive-kopplingen eller kodverktyget: säg det, och be ägaren spara
filen själv och ge dig filens id. Hieratek läser aldrig mallen.

## Kalkyl och utkast

4. Samla det kalkylen behöver: ytor eller mängder, underlag, behandling ur
   prislistan och antal strykningar. Fråga samlat efter det som saknas, en gång.
5. Anropa `calculation_prepare` med ärendets referens, aktuella revision och
   regelversionen som verktygen lämnat. Gissa aldrig referenser eller
   versioner.
6. Anropa `quote_prepare` med kalkylens referens. Ange i presentation det
   ägaren har sagt om jobbet: en kort beskrivning, jobbets adress och ett
   läsbart namn per objekt, till exempel "Kök, väggar". Skriv med ägarens
   ord och lägg inte till något. Utkastet sparas då på servern med
   företagets godkända offertprofil, beställaren ur kundregistret, datum,
   offertnummer och sista giltighetsdag. Koppla jobbet till kunden med
   `case_customer_link` först, annars saknas beställaren.

## Visa resultatet

Börja alltid med läget, med de här orden:

- **Utkast sparat. Ingenting har skickats.**
- Företag, jobb och offertens version, ur verktygens svar.
- Totalsumman som verktyget räknat fram, och vad som är osäkert.

## PDF

Hämta utkastet med `document_get`. Texten är offerten som kunden ska få:
företagets uppgifter, beställaren, arbetet, raderna, beloppen och ägarens
villkor. Gör en PDF av exakt den texten, om din miljö kan skapa filer.

- **Med egen mall** (template i svaret från `document_get`, alltså mallen
  som var godkänd när utkastet sparades, inte profilens nuvarande): hämta filen ur
  företagets Drive med användarens egen Drive-koppling och räkna dess
  SHA-256. Stämmer den inte med utkastets mall: stanna och säg att filen
  har ändrats sedan offerten sparades. Annars fyll mallen med exakt
  utkastets innehåll, på mallens platser för samma uppgifter. Behåll
  mallens logotyp, färger och typsnitt, men ta bort exempeltext,
  exempelrader och exempelbelopp som mallen själv har. Lägg aldrig till,
  ta bort eller ändra rader, belopp eller villkor.
- **Utan mall:** gör en ren standardlayout: rubriken "Offert", företagets
  uppgifter överst, beställaren, arbetet, tabellen, priset och sist
  villkoren.

Utkastets PDF är för ägarens granskning. Ge filen ett namn med
"Offertutkast" och offertnumret, så att den inte förväxlas med den
utfärdade. Saknar miljön filstöd: visa texten och säg att PDF kan skapas i
Claude på webben eller i appen.

## Slutlig offert

När ägaren är nöjd med utkastet blir det den slutliga offerten i två steg:

1. Ägarens beslut. Begär länken med `decision_link_request` och ge den till
   användaren. Ägaren godkänner exakt den versionen på beslutssidan. Ditt
   eget ja ersätter aldrig beslutssidan.
2. Utfärda. När ägaren säger att den är godkänd: anropa `quote_execute` med
   beslutets referens. Hieratek sparar då exakt den godkända versionen som
   slutlig offert. Säg: **Offerten är utfärdad. Ingenting har skickats.**

Gör en PDF av den utfärdade texten på samma sätt som ovan, i ägarens mall
eller i standardlayouten, och ge filen ett namn med "Offert" och
offertnumret. Ägaren skickar den själv till sin kund.

## Spara kopian i företagets Drive

Spara PDF:en i företagets egen Drive med användarens egen Drive-koppling i
Claude. Registrera sedan var den ligger med `case_record_save` och familjen
document_copy: dokumentets referens som postens nyckel, dokumentets
kontrollsumma från `document_get`, filens id och SHA-256 och formatet.
Saknas Drive-kopplingen: be ägaren spara filen själv och ge dig länken.
Hieratek läser eller ändrar aldrig filen; säg att kopian är registrerad, inte
att den är kontrollerad.

## Kundens svar

Svaret på utfärdandet ger en svarslänk. Ge den till ägaren och säg att
kundens ja, nej eller önskade ändring registreras där när kunden har svarat.
Ett ja gör jobbet till ett beställt jobb, som fältrapport, tillägg och
fakturaunderlag sedan bygger på. Läs vad som är registrerat med
`quote_response_list` och `quote_response_get`. Påstå aldrig att något är
skickat, godkänt eller accepterat innan verktygen visar det.

## När något stoppar

- `TERMS_NOT_ACCEPTED`: företaget har inte godkänt villkoren. Ge ägaren
  länken i svaret; ett tryck där räcker. Spara inget förrän det är gjort.
- `QUOTA_REACHED`: månadens sparade arbeten är slut på företagets nivå.
  Förklara det och att läsning och export fungerar som vanligt.
- `CONTEXT_STALE` eller versionskonflikt: läs ärendet igen och fråga innan
  du fortsätter.
- Ett okänt utfall: läs status, försök igen med exakt samma
  idempotensnyckel och skapa ingen ny beställning.
