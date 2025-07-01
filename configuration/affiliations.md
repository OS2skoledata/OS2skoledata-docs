---
title: Lønkontrol
layout: default
parent: Konfiguration
nav_order: 7
has_children: false
---
# Lønkontrol (on-premise)

| Sti | Beskrivelse | Standardværdi |
| --- | --- | --- |
| JobSettings.FullSyncCron | Cron-udtryk for fuld synkronisering | 0 43 2 \* \* ? \* |
| SyncSettings.FetchDataFrom | Datakilde – én af: OPUS, SQL, SOFD |     |
| SyncSettings.OpusWagesFile | Filsti til OPUS-løndata (kræves ved OPUS) |     |
| SyncSettings.SQLConnectionString | SQL forbindelse til database (kræves ved SQL) |     |
| SyncSettings.SQLStatement | SQL-statement til udtræk (kræves ved SQL) |     |
| SyncSettings.SOFDBaseUrl | Base URL til SOFD (kræves ved SOFD) |     |
| SyncSettings.SOFDApiKey | API-nøgle til SOFD (kræves ved SOFD) |     |
| OS2skoledataSettings.BaseUrl | Base URL til OS2skoledata API |     |
| OS2skoledataSettings.ApiKey | API-nøgle til OS2skoledata |     |
| ActiveDirectorySettings.ActiveEmployeesSecurityGroupDN | DistinguishedName for AD-gruppe til aktive medarbejdere, der skal vedligeholdes af denne sync |     |
| ActiveDirectorySettings.CprField | Felt i AD til CPR-nummer | employeeID |
| ActiveDirectorySettings.EmployeeSecurityGroupDN | DistinguishedName for AD-gruppe med alle medarbejdere |     |