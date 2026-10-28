---
name: bevakning
description: Spara och följ upp garantier, besiktningar, åtgärdsfrister, dokumentationskrav och ägarens beslut på ett jobb hos Hieratek. Använd när användaren nämner garanti, besiktning, reklamationsfrist, något som ska följas upp, en checklista eller ett beslut som ska kommas ihåg.
---

# Bevakningar

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Hitta jobbet med `case_list` och läs det med `case_get`.

## Garanti, besiktning och frist

Spara med `case_record_save` och typen warranty_obligation. Ange datumets
källa: står det i avtal eller handling, är det företagets egen regel, eller
har ägaren bekräftat det. Räkna aldrig fram en rättslig frist själv; är
datumet okänt sparas det som okänt och syns som något att kontrollera.

## Dokumentation och beslut

- En checklista för vad jobbet ska dokumenteras med: typen
  documentation_checklist. Listan intygar inte att arbetet håller kvalitet.
- Ett beslut ägaren har tagit, till exempel att tacka nej eller välja
  leverantör: typen owner_decision. Det är ett minne, aldrig ett tillstånd
  att göra något.
- Något ägaren vill att du ska komma ihåg om företaget: typen
  company_memory. Läs det sedan med `company_context_guide`.

## Följa upp

`case_record_list` med typen warranty_obligation visar vad som förfaller,
med de närmaste först. En bevakning är en påminnelse åt ägaren.
Ingenting har skickats till kunden.
