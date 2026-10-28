---
name: efterkalkyl
description: Jämför kalkylerade och faktiska timmar över företagets avslutade jobb hos Hieratek och föreslå nya tidsnormar eller nytt timpris för prislistan, som ägaren godkänner. Använd när användaren undrar om kalkylerna stämmer, vill se hur jobben gick, eller vill justera prislistan efter verkligt utfall.
---

# Efterkalkyl och kalibrering

Inget ändras förrän ägaren godkänner en ny prislista på prislistesidan.
Gamla kalkyler och offerter behåller sina regler. Ingenting har skickats.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.

## Tid på ett jobb

Efterkalkylen bygger på jobbets tidrapport. Spara den med
`time_report_submit`: varje pass med start, slut och rast. Personen anges
bara med en neutral referens; ingen bedöms utifrån sina timmar. Har jobbet
flera behandlingar, till exempel väggar och tak, fråga hur timmarna
fördelades på offertens delar och spara det med `case_record_save` som
timfördelning (time_allocation) för jobbet: alla delar, summan lika med
tidrapporten. Säg om fördelningen kommer ur tidraderna eller är ägarens
uppskattning; en uppskattning räknas aldrig som verifierad.

## Underlag och förslag

2. Hämta underlaget med `calibration_get`. Visa per jobb kalkylerade och
   faktiska timmar och kvoten mellan dem, och säg vilka jobb som är
   avslutade, accepterade och bundna till underlag.
   Vill ägaren titta närmare på ett jobb: hitta det med `case_list`.
3. Visa varje förslag med nuvarande värde, föreslaget värde, antal jobb,
   spridning och säkerhet. Under fem jobb med samma behandling föreslås
   inget, och ett jobb med flera behandlingar räknas bara med en
   timfördelning; säg det och föreslå inget eget värde. Låg säkerhet är ett
   underlag att diskutera, inte en rekommendation.
4. Vill ägaren gå vidare: ge proposed_catalog oförändrad till
   `price_list_propose`, och ge ägaren länken. Ägaren godkänner exakt den
   listan på sidan. Ändra aldrig själv i förslaget, och bedöm aldrig någon
   anställd utifrån utfallet.
