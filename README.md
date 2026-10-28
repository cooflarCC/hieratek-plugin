# Hieratek för Claude

Version 0.7.0

Hieratek är verktyg och arbetsinstruktioner för företagets egen Claude:
offert, prislista, planering, tillägg, kunder, bevakning och
bokföringsunderlag mot företagets sparade uppgifter hos Hieratek. Du behöver
en inbjudan från Hieratek för att logga in.

## Installera en gång

I Claude på webben eller i appen:

1. Öppna **Anpassa > Plugins**.
2. Välj **Lägg till > Lägg till marknadsplats** och skriv
   `cooflarCC/hieratek-plugin`.
3. Slå på **Synka automatiskt** för marknadsplatsen.
4. Lägg till **Hieratek** från marknadsplatsen.
5. Öppna pluginens flik **Connectors**, anslut **hieratek** och logga in med
   e-postadressen från din inbjudan.

Har du tidigare laddat upp Hieratek som zip-fil: ta bort den under
**Anpassa > Plugins** först, så att bara versionen från marknadsplatsen finns.

I Claude Code:

```bash
claude plugin marketplace add cooflarCC/hieratek-plugin
claude plugin install hieratek@hieratek
```

Slå sedan på automatisk uppdatering för marknadsplatsen under `/plugin`,
fliken Marketplaces.

## Uppdateringar

Nya versioner kommer automatiskt när marknadsplatsen synkas. Du behöver inte
ladda upp något. Verktygen på Hierateks server uppdateras direkt för alla;
pluginen bär arbetsinstruktionerna och serverns adress.
