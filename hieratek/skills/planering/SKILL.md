---
name: planering
description: Planera veckans jobb mot neutrala fakta och SMHI:s väderprognos, och lämna planen till ägaren för beslut, mot företagets sparade uppgifter hos Hieratek. Använd när användaren vill planera veckan, fördela jobb på arbetslag, eller undrar om vädret tillåter utomhusarbete.
---

# Veckoplanering och väder

Planen är ett utkast tills ägaren godkänner exakt den versionen på
planeringssidan. Inget bokas. Säg: Ingenting har skickats.

## Före första steget

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Hitta jobben med `case_list`. Fråga efter det som saknas: tider,
   arbetslag, behörigheter och tillgänglighet. Använd bara neutrala
   planeringsfakta; bedöm aldrig någons prestation eller beteende.

## Väder

3. För utomhusjobb: bedöm vädret med `weather_assess` för arbetsplatsens
   koordinater och den dag jobbet är tänkt. Har företaget inga bekräftade
   vädergränser visar verktyget Hierateks förslag: läs upp dem och fråga
   "Vill du använda de här gränserna?". Spara ägarens svar med
   `case_record_save` som företagets vädergränser och bedöm igen.
   Säg för varje dag om den är lämplig, ska bevakas, är olämplig och
   varför, eller är okänd, och nämn de föreslagna alternativa dagarna.
   Ägaren väljer dagen. En dag utan prognos är okänd, aldrig bra väder.
   `weather_forecast_get` ger bara prognosen utan bedömning.

## Plan

4. Spara fakta med `planning_facts_record`. Ange vädret med prognosens
   källa, utfärdandetid och sluttid, och det läge ägaren angav.
5. Spara fördelningen med `planning_draft_record` och läs upp planen och
   dess varningar.
6. Hämta planen med `planning_get` och ge ägaren länken. Där granskas och
   godkänns exakt den versionen. Ändras något krävs ett nytt godkännande.
