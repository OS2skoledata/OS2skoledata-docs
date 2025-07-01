---
title: AD opsætning
layout: default
nav_order: 1
parent: Opsætning
has_children: false
---

# Formål

Dette dokument er rettet mod teknikere der skal opsætte og konfigurere kommunens integration fra OS2skoledata til AD, så brugeroplysninger bliver holdt ved lige med stamdata fra OS2skoledata.

## Forudsætninger

### Windows Server

Servicen skal installeres på en Windows server 2016 eller nyere med:

- Netværksmæssig adgang til kommunens AD

- Netværksmæssig adgang til OS2skoledata via HTTPS

Service bruger en meget begrænset mængde resourcer, så længe der er RAM, CPU og Disk nok til at afvikle windows, så er det fint til servicen.

### Service konto i AD

Der skal oprettes en service konto i kommunes AD.

Kontoen skal have adgang til at oprette, nedlægge og ajourføre brugerkonti, grupper og OU'ere i AD'et. Hvis der anvendes et beskyttet felt til CPR nummeret, så skal der ligeledes gives adgang til at læse og skrive i dette felt. Kontoen skal have adgang fra at flytte brugere fra over alt i AD'et over i OS2skoledata strukturen.

## API bruger til OS2skoledata

Der skal oprettes en systemadgang til OS2skoledata. Dette opsættes i samarbejde med Digital Identity.

# Installation af Windows Service

## Download service

Download og installér servicen fra <https://www.os2skoledata.dk/download.html>

## Konfiguration af service

Konfiguration af servicen foretages i filen **appsettings.json** som ligger i roden af installationsmappen (default C:\Program Files (x86)\Digital Identity\OS2skoledataADSync).

Læs mere om alle konfigurationsmuligheder i dokumentet vedrørende konfiguration.

## Start af service

Servicen skal konfigureres til at afvikle under den servicekonto som har de fornødne rettigheder, og herefter kan den startes som en normal service under Services.

Det anbefales at man sætter den til automatisk opstart (gerne med forsinket opstart), så man er sikker på at den kører efter en server genstart.

Ved start/genstart af servicen foretages altid en fuld synkronisering af data, ellers kører den med regelmæssige delta-opdateringer som angivet i konfigurationsfilen, og en tilsvarende fuld synkronisering som angivet i samme konfigurationsfil.

Det er derfor en god idé at kigge i logfilen om alt er gået godt. Logfilens placering kan ses i indstillingen **serilog:write-to:RollingFile.pathFormat**.
