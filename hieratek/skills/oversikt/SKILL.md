---
name: oversikt
description: Visa vad företaget behöver ta tag i i jobben, offerterna, leadsen, bevakningarna och besluten, ur företagets sparade uppgifter hos Hieratek. Använd när användaren frågar vad som väntar eller är på gång i företaget, i firman, i jobben eller i Hieratek, vill se läget i verksamheten eller prioritera arbetsdagen. Gäller företagets ärenden, inte privat kalender eller mejl.
---

# Översikt

Arbeta alltid mot företagets sparade uppgifter hos Hieratek. Visa bara det
verktygen svarar; hitta aldrig på ärenden, belopp eller datum.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Anropa `morning_overview` för företagets öppna jobb och leads.
3. För de jobb som verkar viktigast: läs `task_list` för ärendet. Där står
   beslut som väntar på ägaren, till exempel en offert att godkänna.
   Läs också `document_list` för samma ärende: där står om ett offertutkast
   eller en utfärdad offert redan finns, och vilken version.
4. Läs bevakningar som förfaller snart med `case_record_list` och typen
   warranty_obligation.

## Visa resultatet

Börja med det som väntar på ägaren, sedan det som förfaller, sist resten.
Högst fem rader först; mer bara om användaren vill.

För varje rad: jobbet, läget med vanliga ord och nästa steg. Lägena är:

- **Väntar på ditt beslut**: något ligger på beslutssidan.
- **Utkast**: sparat internt, ingenting är skickat. Ur `document_list`:
  ett aktuellt utkast (current) med status needs_decision väntar på ägarens
  granskning och godkännande; med status pending är det godkänt och väntar
  på att utfärdas; med status completed är offerten utfärdad. Finns inget
  aktuellt utkast, bara äldre eller inga alls, och har ärendet läget lead,
  draft eller quoted enligt `case_get`, är nästa steg ett nytt
  offertutkast. Ett ärende i läget accepted, där kundens ja är registrerat,
  eller closed behöver ingen ny offert. Säg inte om kalkylen finns; det syns inte i de här
  verktygen, utan i offertflödet.
- **Klart**: verktyget visar ett kvitto.

Avsluta med ett förslag på vad ägaren kan göra först, och fråga om du ska
börja där. En översikt ändrar ingenting; säg vid behov:
Ingenting har skickats. Behöver du ett jobb som inte syns: sök med `case_list`.
