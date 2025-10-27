---
title: ASM
layout: default
parent: Konfiguration
nav_order: 5
has_children: false
---
# Apple School Manager

| Sti | Beskrivelse | Standardværdi |
| --- | --- | --- |
| JobSettings.FullSyncCron | Cron-udtryk for fuld synkronisering | 0 43 2 \* \* ? \*|
| DryRun | Bestemmer om filerne skal gemmes på computeren, hvor servicen køres fra i stedet for at uploade dem til Apple | false|
| DryRunFilePath | | | 
| OS2skoledataSettings.BaseUrl | Base URL til OS2skoledata API |     |
| OS2skoledataSettings.ApiKey | API-nøgle til OS2skoledata. Der kan via OS2skoledata brugergrænsefladen oprettes en klient med typen "Adgang til API'erne bortset fra import API'et". |     |
| AppleSchoolManagerSettings.Domain | Domænenavnet (bruges til email på brugere) | |
| AppleSchoolManagerSettings.ZipFileName | Navn på zipfilen, der uploades til Apple | |
| AppleSchoolManagerSettings.SFTP.Url | URL til SFTP | |
| AppleSchoolManagerSettings.SFTP.Username | Brugernavn til SFTP | |
| AppleSchoolManagerSettings.SFTP.Password | Kodeord til SFTP | |