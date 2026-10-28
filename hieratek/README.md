# Hieratek

Verktyg och arbetsinstruktioner för kundens egen Claude. Pluginen kopplar
Claude till företagets sparade uppgifter hos Hieratek och ger fjorton
arbetssätt:

- **oversikt**: vad som väntar på ägaren, vad som förfaller och hur jobben står;
- **offert**: från jobb och kalkyl till godkänd slutlig offert, PDF i företagets Drive och kundens svar.
  Offerten visar företagets offertprofil, beställaren, datum, offertnummer,
  sista giltighetsdag och ägarens egna villkor, på svenska. Ägaren godkänner
  profilen på en egen sida och kan ladda upp sin egen offertmall (Word, PDF
  eller bild), som Claude fyller med exakt offertens innehåll. Utan mall blir
  det en ren standardlayout;
- **andra-offert**: en ändring sparas som ny version bredvid den gamla;
- **fortsatt**: återuppta i en ny chatt utifrån det som är sparat;
- **planering**: veckoplanering med SMHI:s prognos bedömd mot företagets vädergränser, och ägarens beslut;
- **tillagg**: fältrapport, tillägg (ÄTA) och fakturaunderlag;
- **inkorg**: mejl läses med användarens egen mejlkoppling, och det som hör
  till verksamheten sparas som lead, risk eller svarsutkast;
- **kunder**: kundregister, kundens jobb och radering på företagets begäran;
- **bevakning**: garantier, besiktningar, frister, checklistor och beslut;
- **bokforing**: kvitton och fakturor som underlag med konteringsutkast;
- **kalender**: en kalenderfil som ägaren själv lägger in; ingenting bokas;
- **inmatning**: jobbets rum, väggar och mått med fasta nummer och en principskiss;
- **prisimport**: prislistan ur det ägaren redan har, som egna prislistor,
  gamla offerter, kalkyler och leverantörens priser; ägaren godkänner listan
  på en egen sida;
- **efterkalkyl**: kalkylerade mot faktiska timmar över flera jobb och förslag på nya normar som ägaren godkänner.

Första gången godkänner ägaren villkoren med ett tryck på sidan som
verktygen länkar till; innan dess sparas ingenting.

Kalkylen räknas av Hierateks verktyg. Ingenting skickas till kunder utan
ägarens beslut på beslutssidan.

## Installera

Pluginen installeras från den publika marknadsplatsen
`cooflarCC/hieratek-plugin` och uppdateras sedan automatiskt. I Claude på
webben eller i appen: **Anpassa > Plugins > Lägg till > Lägg till
marknadsplats**, skriv `cooflarCC/hieratek-plugin`, slå på **Synka
automatiskt** och lägg till Hieratek. Lägg sedan till anslutningen under
pluginens **Connectors** och logga in med företagets inbjudan.

Använder företaget Claudes egna kopplingar till Google Drive, Gmail eller
Google Kalender: öppna **Anpassa > Connectors**, välj kopplingen och sätt
verktygen som raderar till blockerade under dess verktygsbehörigheter. Det
gäller Drive `trash_file`, Gmail `trash_message`, `trash_thread` och
`delete_label` samt Kalender `delete_event`. Läsa och skapa ska vara
tillåtet, eftersom offerter och underlag sparas i företagets Drive. Har
företaget en organisation i Claude låser administratören samma inställning
för alla. Spärren i kopplingen gäller i varje chatt, på webben, i appen och
i Claude Code, oavsett var en session startar.

I Claude Code:

```bash
claude plugin marketplace add cooflarCC/hieratek-plugin
claude plugin install hieratek@hieratek
```

Slå på automatisk uppdatering för marknadsplatsen under `/plugin`, fliken
Marketplaces. Vid utveckling går den lokala mappen att lägga till i stället:
`claude plugin marketplace add ./v2/clients/plugin`.

Anslutningen pekar på testmiljöns kundserver tills produktionen finns.
