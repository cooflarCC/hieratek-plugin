---
name: andra-offert
description: Ändra en sparad offert hos Hieratek, till exempel ytor, behandling, antal strykningar eller arbetsmoment, och spara en ny version bredvid den gamla. Använd när användaren vill justera, rätta eller räkna om en offert.
---

# Ändra offert

En ändring är alltid en ny version. Den gamla versionen ligger kvar och kan
läsas, men den är inte längre den aktuella.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Hitta jobbet med `case_list` och läs det med `case_get`.
3. Lista offertens versioner med `document_list` och läs den senaste med
   `document_get`. Säg vilken version du utgår från.
4. Sammanfatta ändringen i en mening och låt användaren rätta dig innan du
   räknar.
5. Räkna om med `calculation_prepare` och den nya indatan, mot ärendets
   aktuella revision. Spara sedan med `quote_prepare`.
6. Visa resultatet:
   - **Utkast sparat som ny version. Ingenting har skickats.**
   - Gammal och ny version, och vad som ändrats i summa och rader.
7. Gör en ny PDF av den nya versionen på samma sätt som i skillen `offert`,
   med det nya versionsnumret i rubriken. Spara och registrera den som i skillen
   `offert`, med den nya versionens referens.

Ändra aldrig en gammal version och blanda aldrig rader från två versioner.
Vill användaren ändra hur företaget räknar i stort, till exempel ett
timpris eller en regel för alla jobb, är det en anpassning: registrera den
med `customization_request` i stället för att räkna om jobbet.

Vid `QUOTA_REACHED`, `CONTEXT_STALE` eller okänt utfall gäller samma regler
som i skillen `offert`.
