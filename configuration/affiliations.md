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
| <span id="JobSettings.FullSyncCron">JobSettings.FullSyncCron</span> | Cron-udtryk for fuld synkronisering | 0 43 2 \* \* ? \* |
| <span id="SyncSettings.FetchDataFrom">SyncSettings.FetchDataFrom</span> | Datakilde – én af: OPUS, SQL, SOFD |     |
| <span id="SyncSettings.OpusWagesFile">SyncSettings.OpusWagesFile</span> | Filsti til OPUS-løndata (kræves ved OPUS) |     |
| <span id="SyncSettings.SQLConnectionString">SyncSettings.SQLConnectionString</span> | SQL forbindelse til database (kræves ved SQL) |     |
| <span id="SyncSettings.SQLStatement">SyncSettings.SQLStatement</span> | SQL-statement til udtræk (kræves ved SQL). Fx "SELECT employee_id, start_date, stop_date, cpr_number AS cpr FROM os2skoledata_checker.dbo.affiliations;". Vi har brug for employee_id, start_date, stop_date og cpr_number|     |
| <span id="SyncSettings.SOFDBaseUrl">SyncSettings.SOFDBaseUrl</span> | Base URL til SOFD (kræves ved SOFD) |     |
| <span id="SyncSettings.SOFDApiKey">SyncSettings.SOFDApiKey</span> | API-nøgle til SOFD (kræves ved SOFD) |     |
| <span id="OS2skoledataSettings.BaseUrl">OS2skoledataSettings.BaseUrl</span> | Base URL til OS2skoledata API |     |
| <span id="OS2skoledataSettings.ApiKey">OS2skoledataSettings.ApiKey</span> | API-nøgle til OS2skoledata. Der kan via OS2skoledata brugergrænsefladen oprettes en klient med typen "Adgang til API'erne bortset fra import API'et" |     |
| <span id="ActiveDirectorySettings.ActiveEmployeesSecurityGroupDN">ActiveDirectorySettings.ActiveEmployeesSecurityGroupDN</span> | DistinguishedName for AD-gruppe til aktive medarbejdere, der skal vedligeholdes af denne sync |     |
| <span id="ActiveDirectorySettings.InactiveEmployeesSecurityGroupDN">ActiveDirectorySettings.InactiveEmployeesSecurityGroupDN</span> | DistinguishedName for AD-gruppe til inaktive medarbejdere, der skal vedligeholdes af denne sync |     |
| <span id="ActiveDirectorySettings.CprField">ActiveDirectorySettings.CprField</span> | Felt i AD til CPR-nummer | employeeID |
| <span id="ActiveDirectorySettings.EmployeeSecurityGroupDN">ActiveDirectorySettings.EmployeeSecurityGroupDN</span> | DistinguishedName for AD-gruppe med alle medarbejdere |     |