---
name: inmatning
description: Bygg jobbets elementkatalog hos Hieratek ur ägarens skiss, foton och mått: rum och fasader, väggar och delar med fasta nummer, vad som är mätt och vad som saknas, och rita en principskiss. Använd när användaren beskriver ett rum eller en fasad, skickar en handritad skiss eller ett foto, eller vill veta vilka mått som saknas inför en kalkyl.
---

# Inmätning och elementkatalog

Katalogen beskriver vad ägaren såg och mätte. Den ändrar inget pris och
ingen kalkyl. Ingenting har skickats.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Hitta jobbet med `case_list` och läs det med `case_get`.
3. Spara först skissen, fotot eller anteckningen i företagets egen Drive
   med användarens Drive-koppling. Saknas kopplingen: be ägaren spara
   filen och ge dig länken. Varje version av katalogen behöver minst en
   sådan fil med id och SHA-256, och tidigare filer ska finnas kvar.
4. Läs befintlig katalog med `case_record_get`, typen element_catalog och
   jobbets referens som nyckel. Bygg hela modellen:
   - rum och fasader som R1, R2, väggar, tak och föremål som E1, E2, och
     delar som ett fönster i en vägg med del av;
   - mått som M1, M2 med enhet. Ett mätt värde säger hur det mättes; en
     uppskattning märks som uppskattad. Saknas måttet lämnas det tomt.
   Ett nummer återanvänds aldrig: nya nummer tar nästa nummer över
   high_water, och high_water sjunker aldrig.
5. Spara med `case_record_save` som ny version och läs upp vad som saknas.
6. Visa skissen med `element_catalog_sketch`. Den är en principskiss, inte
   skalenlig.
7. När jobbet räknas med `calculation_prepare`: koppla varje objekt till
   sitt element med katalogens revision och elementets E-nummer. Offerten
   visar då elementets nummer och namn, så att ägaren och kunden ser vilken
   vägg eller vilket tak varje rad gäller. En senare version av katalogen
   ändrar inte en redan gjord kalkyl.
