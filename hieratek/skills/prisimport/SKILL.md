---
name: prisimport
description: Gör företagets prislista hos Hieratek ur det ägaren redan har, till exempel en egen prislista, gamla offerter, kalkyler, kalkylark, leverantörens prislista, foton av papper eller inklistrad text. Läs underlaget, plocka ut företagets egna värden, visa varifrån varje värde kommer och föreslå hela listan för ägarens godkännande. Använd när ägaren vill ladda upp, importera eller läsa in priser, eller saknar prislista inför första kalkylen.
---

# Prisimport

Du läser underlaget här, i ägarens egen AI-tjänst. Till Hieratek skickas
bara de värden ägaren ser i förslaget, aldrig filerna. Ingenting börjar gälla
förrän ägaren har godkänt prislistan på sidan. Ingenting har skickats.

## Före första steget

1. Anropa `workspace_status` och säg vilket företag du arbetar i, med namnet
   ur svaret. Prislistan hör till företaget och inte till ett jobb, så
   `case_list` behövs inte här.
2. Läs nuvarande prislista med `price_list_get`. Finns en: det här blir en
   ändring, och värden som underlaget inte säger något om behålls som de är.
   Ett nytt förslag ersätter inte ett äldre, och ett äldre förslag kan
   fortfarande godkännas. Säg därför till ägaren att avvisa äldre förslag
   som inte ska gälla, på deras egen sida, innan det nya godkänns.

## Läs underlaget

3. Ta emot det ägaren har: PDF, kalkylark, CSV, Word, foton eller text. Fråga
   för varje dokument vems det är, om det inte framgår. Använd bara
   företagets egna priser och normer, och leverantörens pris på material som
   företaget köper. En annan firmas offert eller prislista används aldrig.
4. Gamla offerter och kalkyler innehåller ofta beställarens namn, adress och
   telefon. Läs förbi dem: skriv inte ut dem, och ta inte med dem i något
   som sparas. Bara priser, tider, mängder och procentsatser behövs.

## Plocka ut värdena

5. Prislistan har de här värdena. Hitta så många du kan.

   | Värde | Enhet i listan | Brukar stå som |
   |---|---|---|
   | Timkostnad | kr per timme | timkostnad, lönekostnad per timme |
   | Direkta kostnader per jobb | kr | etablering, framkörning |
   | Spill | procent | spill, svinn |
   | Omkostnadspåslag | procent | omkostnader, OH, administrationspåslag |
   | Risk | procent av kostnaden eller fast belopp | risk, oförutsett |
   | Prissättning | målmarginal eller påslag, i procent | marginal, vinstpåslag, TB |
   | Rabatt | procent | rabatt |
   | Moms | procent | moms, normalt 25 |

   Per behandling, till exempel väggmålning, takmålning, snickerier eller
   fasad:

   | Värde | Enhet i listan | Brukar stå som |
   |---|---|---|
   | Täckning | kvm per liter och strykning | åtgång, sträckförmåga |
   | Förarbete | timmar per kvm | spackling, slipning, förarbete |
   | Målningstid | timmar per kvm och strykning | tidsnorm, ackord |
   | Materialpris | kr per liter, utan moms | inköpspris, leverantörspris |

   Prislistan bygger på företagets egna kostnader. Kalkylen lägger själv
   på omkostnader, risk och marginal. Ett timpris, en fast avgift eller ett
   materialpris i en offert eller faktura till kund är därför ett
   försäljningspris och får aldrig bli timkostnad, direkt kostnad eller
   materialpris i listan, för då räknas påslaget två gånger. Fråga ägaren
   efter kostnaden i stället, och säg vilket försäljningspris du såg.
   Offerter och kalkyler duger däremot för mängder och tider: åtgång,
   förarbete och tid per strykning.

6. Räkna om till listans enheter och säg att du har gjort det:
   - liter per kvm blir kvm per liter (1 delat med värdet);
   - kvm per timme blir timmar per kvm (1 delat med värdet);
   - minuter blir timmar;
   - pris med moms blir pris utan moms (dela med 1 plus momsen);
   - pris per burk blir pris per liter (dela med burkens liter).
7. Räkna bara fram ett värde när underlaget entydigt ger det, till exempel
   en offertrad med mängd, timmar och timpris. En klumpsumma för ett helt
   jobb går inte att dela upp: fråga i stället. Gissa aldrig, och fyll aldrig
   i ett värde från en annan firma eller från allmän kunskap.
8. Säger två dokument olika: visa båda med datum och fråga vilket som
   gäller. Går ordningen inte att belägga, till exempel när bara det ena
   är daterat, ska ägaren avgöra; föreslå inget av dem själv.

## Visa förslaget innan det sparas

9. Visa en tabell med varje värde i listan: värdet, källan (dokumentets namn
   och sida, rad eller cell) och hur det togs fram: avläst, omräknat eller
   ägarens svar. Skriv under tabellen vilka värden som saknas.
10. Fråga samlat, en gång, efter det som saknas. Underlag- och skickfaktor är
    1 om ägaren inte säger något annat; säg det.
11. Ge behandlingarna korta namn med små bokstäver utan å, ä och ö, till
    exempel vaggmalning och takmalning. Finns listan redan: använd samma
    namn för samma behandling.

## Föreslå

12. Anropa `price_list_propose` med hela listan, även oförändrade värden.
    Ge ägaren länken i svaret och säg vad som ändras mot nuvarande lista.
13. Avsluta med läget: **Prislistan väntar på ditt godkännande. Ingenting
    gäller och ingenting har skickats.** Kalkyler görs först när ägaren har
    godkänt listan på sidan.
