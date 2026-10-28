---
name: kalender
description: Gör en kalenderfil (.ics) av ett planerat arbetspass, ett förbesök eller en bokningsbekräftelse som ägaren själv lägger in i sin kalender. Använd när användaren vill lägga något i kalendern, boka in ett jobb eller spara en tid.
---

# Kalender

Hieratek bokar ingenting. Du gör en kalenderfil som ägaren själv öppnar och
lägger in. Påstå aldrig att något är bokat: det som finns är en fil.

1. Anropa `workspace_status` och säg vilket företag du arbetar i.
2. Hitta jobbet med `case_list`. Gäller det ett planerat pass: läs planen med
   `planning_get` och använd bara den godkända planens dagar och tider.
3. Står tiden i en bokningsbekräftelse eller ett mejl: använd exakt den
   tiden. Går den inte att läsa ut: fråga, gissa aldrig.
4. Gör en `.ics`-fil med jobbets namn som rubrik, plats om den finns, och
   tiden i svensk tid. Lägg inte in kundens personuppgifter mer än jobbet
   kräver.
5. Säg: **Kalenderfilen är klar. Öppna den för att lägga in tiden.
   Ingenting har skickats och ingenting är bokat.**

Saknar din miljö filstöd: visa tiden och rubriken så att ägaren kan lägga in
den själv, och säg att filen kan skapas i Claude på webben eller i appen.
