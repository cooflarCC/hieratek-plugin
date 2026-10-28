---
name: bokforing
description: Förbered kvitton och leverantörsfakturor som bokföringsunderlag med konteringsutkast och visa månadens förkonteringslista hos Hieratek. Använd när användaren har ett kvitto, en faktura eller ett underlag till bokföringen, eller vill se månadens underlag.
---

# Bokföringsunderlag

Bokföringsprogrammet och banken är sanningen. Hieratek förbereder bara
underlag. Påstå aldrig att något är bokfört, betalt eller infört.

1. Anropa `workspace_status` och säg vilket företag du arbetar i. Hör
   underlaget till ett jobb: hitta det med `case_list`.
2. Originalet sparas först i företagets egen Drive, med användarens egen
   Drive-koppling i Claude. Saknas kopplingen: be ägaren spara originalet
   själv och ge dig länken.
3. Läs kvittot eller fakturan. Fråga om momsen när den inte framgår:
   vanlig svensk moms, omvänd skattskyldighet för byggtjänst, eller ingen
   moms. Gissa aldrig.
4. Spara underlaget med `case_record_save` och typen accounting_document,
   med länken till originalet som källa.
5. Visa: **Utkast. Ingenting är bokfört och ingenting har skickats.** Konteringen är ett förslag som
   ägaren eller redovisningskonsulten för in själv.

## Månadens lista

`accounting_month` visar månadens underlag efter dokumentdatum, med möjliga
dubbletter markerade. Det är en lista att skriva av, inget mer.
