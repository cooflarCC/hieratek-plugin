---
name: fortsatt
description: Återuppta arbetet med företagets jobb och offerter i en ny chatt, utifrån det som är sparat hos Hieratek. Använd när användaren skriver fortsätt, var var vi, vad händer med jobbet, eller frågar om läget för en offert.
---

# Fortsätt där ni var

Chatten minns inget från förra gången; det som gäller är det som är sparat
hos Hieratek. Bygg aldrig vidare på något som bara stod i en tidigare chatt.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Visa företagets läge med `morning_overview`, eller lista öppna jobb med
   `case_list` om användaren frågar om ett visst jobb.
3. När jobbet är valt: läs det med `case_get`, offertens versioner med
   `document_list` och vad som väntar med `task_list`.
4. Sammanfatta i högst fem rader:
   - jobbet och offertens senaste version;
   - läget: utkast, väntar på ditt godkännande eller genomfört, med orden
     "Ingenting har skickats" när det är sant;
   - vad som väntar på vem;
   - ett förslag på nästa steg.
5. Spara `continuation_ref` från `case_get` och använd den när du läser
   samma jobb igen. Får du `CONTEXT_STALE`: läs jobbet på nytt och utgå från
   de aktuella uppgifterna.

Är något oklart, till exempel två jobb med liknande namn, fråga vilket som
avses innan du läser eller ändrar något.
