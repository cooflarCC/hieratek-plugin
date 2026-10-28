---
name: tillagg
description: Rapportera vad som gjorts på ett jobb, räkna fram ÄTA för tillkommet eller utgått arbete och ta fram fakturaunderlaget, mot företagets sparade uppgifter hos Hieratek. Använd när användaren berättar vad som blev gjort, nämner tilläggsarbete, ÄTA, något som utgick, eller vill fakturera ett jobb.
---

# Fältrapport, ÄTA och fakturaunderlag

Beloppen räknas av Hierateks verktyg ur jobbets offert; räkna aldrig fram
dem själv.

## Före första steget

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Hitta jobbet med `case_list` och läs det med `case_get`.

## Fältrapport

3. Fråga vad som utfördes, vad som tillkom och vad som utgick, per del av
   jobbet, med mängd och enhet. Delarna heter som i offerten; läs dem med
   `document_get` om du behöver.
4. Spara hela rapporten med `field_report_record`. Ange alltid alla rader,
   även de som inte ändrats.
5. Läs upp raderna för ägaren och fråga uttryckligen: "Stämmer det här med
   vad som gjordes?" Först efter ett tydligt ja registrerar du bekräftelsen
   med `field_report_confirm`. Ditt eget antagande räknas aldrig.

## ÄTA

6. Fråga om tillägget gäller fast pris eller löpande räkning, och anropa
   `change_order_prepare`. Löpande räkning är en uppskattning, aldrig ett
   fast belopp.
7. Visa beloppet och fråga ägaren om ÄTA:n får lämnas till kunden.
   Registrera svaret med `change_order_decide` som ägarens beslut.
8. När kunden har svarat: registrera svaret med `change_order_decide` som
   kundens svar, med hur det kom in. Ingenting har skickats av verktygen;
   ägaren lämnar själv ÄTA:n till kunden.

## Fakturaunderlag

9. Anropa `invoice_basis_prepare`. Säg vad som saknas, med vardagliga ord,
   och vad som behövs för att fylla det. Underlaget är aldrig bokfört eller
   skickat.

## Läget, varje gång

Börja varje svar med läget: **Utkast**, **Väntar på ditt godkännande** eller
**Genomfört**, och skriv "Ingenting har skickats" när det är sant. Läs
nuläget med `field_report_get`, `change_order_get` och `invoice_basis_get`.

## När något stoppar

- `FIELD_CONFIRMATION_REQUIRED`: ägaren har inte bekräftat fältrapporten.
- `CHANGE_ORDER_BLOCKED`: arbete utanför offerten måste beslutas för sig.
- `FIELD_REPORT_STALE` eller `CHANGE_ORDER_STALE`: läs nuläget igen och
  fråga innan du fortsätter.
