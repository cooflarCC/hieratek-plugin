---
name: oversikt
description: Visa vad företaget behöver ta tag i, hur jobben står och vad som väntar på ägarens beslut, ur företagets sparade uppgifter hos Hieratek. Använd när användaren säger hej, frågar vad som är på gång, vill se läget, behöver dig nu, prioritera eller få en översikt.
---

# Översikt

Arbeta alltid mot företagets sparade uppgifter hos Hieratek. Visa bara det
verktygen svarar; hitta aldrig på ärenden, belopp eller datum.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Anropa `morning_overview` för företagets öppna jobb och leads.
3. För de jobb som verkar viktigast: läs `task_list` för ärendet. Där står
   beslut som väntar på ägaren, till exempel en offert att godkänna.
4. Läs bevakningar som förfaller snart med `case_record_list` och typen
   warranty_obligation.

## Visa resultatet

Börja med det som väntar på ägaren, sedan det som förfaller, sist resten.
Högst fem rader först; mer bara om användaren vill.

För varje rad: jobbet, läget med vanliga ord och nästa steg. Lägena är:

- **Väntar på ditt beslut**: något ligger på beslutssidan.
- **Utkast**: sparat internt, ingenting är skickat.
- **Klart**: verktyget visar ett kvitto.

Avsluta med ett förslag på vad ägaren kan göra först, och fråga om du ska
börja där. En översikt ändrar ingenting; säg vid behov:
Ingenting har skickats. Behöver du ett jobb som inte syns: sök med `case_list`.
