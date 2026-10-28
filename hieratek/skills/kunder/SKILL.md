---
name: kunder
description: Lägg upp, rätta, hitta eller radera företagets kunder och se en kunds jobb, offerter och fakturaunderlag hos Hieratek. Använd när användaren nämner en kund, vill se en kunds historik, rätta kontaktuppgifter eller ta bort en kunds uppgifter.
---

# Kunder

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Sök med `customer_list` innan du lägger upp en ny kund, så att samma kund
   inte läggs upp två gånger. Visa träffarna och låt ägaren välja.
3. Ny kund eller rättelse: `customer_save` med bara de uppgifter som behövs
   för jobbet. Spara aldrig personnummer eller annat som inte behövs.
4. Koppla ett jobb till kunden med `case_customer_link`, först när ägaren
   uttryckligen har sagt vilken kund jobbet gäller. Hitta jobbet med
   `case_list`.
5. Kundens historik: `customer_get`. Visa jobben med läge, offertbelopp och
   kundens svar.

## Radera en kund

Bara på företagets egen begäran. Säg först vad som händer: kundens namn och
kontaktuppgifter tas bort för gott, jobben finns kvar utan namn, och det kan
inte ångras. Fråga uttryckligen: "Ska jag radera kundens uppgifter?" Först
efter ett tydligt ja: `customer_erase`.

Inget av detta kontaktar kunden: ingenting har skickats.
