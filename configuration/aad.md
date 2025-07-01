---
title: AAD
layout: default
parent: Konfiguration
nav_order: 4
has_children: false
---

# Azure AD integration

| Sti | Beskrivelse | Standardværdi |
| --- | --- | --- |
| skole.azure-ad.clientID | Klient-ID for Azure AD-applikationen. |     |
| skole.azure-ad.clientSecret | Klienthemmelighed til Azure AD-applikationen. |     |
| skole.azure-ad.usingPEMCertificate | Brug PEM certifikat for adgang til Azure. Kræver udfyldning af skole.azure-ad.certificatePath | false |
| skole.azure-ad.certificatePath | Bruges kun hvis skole.azure-ad.usingPEMCertificate er ”true”. Ruten til PEM certifikatet. |     |
| skole.azure-ad.tenantID | Tenant-ID for Azure AD. |     |
| skole.azure-ad.userDryRun | Opret grupper og teams uden at udføre handlinger med brugere. | false |
| skole.azure-ad.teamsAndGroupsOnly | Synkroniser kun teams og grupper – håndter ikke brugere | false |
| skole.os2skoledata.apiKey | API-nøgle til OS2skoledata. |     |
| skole.os2skoledata.baseUrl | URL til OS2skoledata API. |     |
| skole.syncSettings.domain | Domæne – bruges fx til email |     |
| skole.syncSettings.useUsernameAsKey | Brug brugernavn som nøgle I stedet for cpr | false |
| skole.syncSettings.uniIdField | Felt på burgere i Azure AD til Uni-login. Mulige:  <br>NONE, DEPARTMENT, EMPLOYEE_ID | NONE |
| skole.syncSettings.usernameSettings.usernameStandard | Strategi til opbygning af brugernavne for nye brugere. Se sektion omkring brugernavnestandarder. |     |
| skole.syncSettings.usernameSettings.usernamePrefix | Præfiks til brugernavne, hvis brugernavnestandarden understøtter det |     |
| skole.syncSettings.usernameSettings.randomStandardLetterCount | Antal bogstaver brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| skole.syncSettings.usernameSettings.randomStandardNumberCount | Antal tal I brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| skole.syncSettings.filteringSettings.globallyExcludedRoles | Roller der altid ekskluderes fra oprettelse | \[\] |
| skole.syncSettings.filteringSettings.exludedRolesInInstitution | Institutionsspecifik eksklusion. | {}  |
| skole.syncSettings.nameStandards.allInInstitutionSecurityGroupNameStandard | Navnestandard for sikkerhedsgruppen for alle brugere i institutionen. |     |
| skole.syncSettings.nameStandards.allStudentsInInstitutionSecurityGroupNameStandard | Navnestandard for sikkerhedsgruppen for alle elever i institutionen. |     |
| skole.syncSettings.nameStandards.allEmployeesInInstitutionSecurityGroupNameStandard | Navnestandard for sikkerhedsgruppen for alle medarbejdere i institutionen. |     |
| skole.syncSettings.nameStandards.classSecurityGroupNameStandard | Navnestandard for sikkerhedsgruppen for alle i en klasse |     |
| skole.syncSettings.nameStandards.classSecurityGroupNameStandardNoClassYear | Navnestandard for ovenstående gruppe, der anvendes hvis klassen ikke har startår |     |
| skole.syncSettings.nameStandards.globalEmployeeSecurityGroupName | Navnestandard for global medarbejdergruppe. |     |
| skole.syncSettings.nameStandards.globalStudentSecurityGroupName | Navnestandard for global elevgruppe. |     |
| skole.syncSettings.nameStandards.allEmployeesInInstitutionTeamNameStandard | Navnestandard for team for ansatte. |     |
| skole.syncSettings.nameStandards.allEmployeesInInstitutionTeamMailStandard | Navnestandard for mail til team med ansatte. |     |
| skole.syncSettings.nameStandards.classTeamNameStandard | Navnestandard for team for klasse. |     |
| skole.syncSettings.nameStandards.classTeamNameStandardNoClassYear | Navnestandard for ovenstående team, der anvendes hvis klassen ikke har startår |     |
| skole.syncSettings.nameStandards.classTeamMailStandard | Navnestandard for mail til klasseteam. |     |
| skole.syncSettings.nameStandards.classTeamMailStandardNoClassYear | Navnestandard for mail til ovenstående team, der anvendes hvis klassen ikke har startår |     |
| skole.syncSettings.nameStandards.levelSecurityGroupNameStandard | Navnestandard for klassetrin-gruppe |     |
| skole.syncSettings.nameStandards.globalLevelSecurityGroupNameStandard | Navnestandard for global klassetring-gruppe |     |
| skole.syncSettings.azureTeamsSettings.handleTeams | Aktiverer synkronisering af Teams | false |
| skole.syncSettings.azureTeamsSettings.readOnlyPeriod | Antal dage et team skal være skrivebeskyttet inden det slettes | 90  |
| skole.syncSettings.azureTeamsSettings.classTeamTemplate | Navn på Team-skabelon for klasser. | educationClass |
| skole.syncSettings.azureTeamsSettings.employeeTeamTemplate | Navn på Team-skabelon for ansatte. | standard |
| skole.syncSettings.deleteUserSettings.enabled | Aktiver automatisk fuld sletning af brugere. | false |
| skole.syncSettings.deleteUserSettings.daysBeforeDeletionStudent | Dage før elev slettes efter den er disabled | 60  |
| skole.syncSettings.deleteUserSettings.daysBeforeDeletionEmployee | Dage før ansat slettes efter den er disabled | 60  |
| skole.syncSettings.deleteUserSettings.daysBeforeDeletionExternal | Dage før ekstern slettes efter den er disabled | 60  |
| cron.deltaSync | Cron udtryk for hvornår der skal køres delta sync | 0 0/5 \* \* \* ? |
| cron.fullSync | Cron udtryk for hvornår der skal køres fuld sync | 0 10 1 \* \* ? |
| cron.teamsAndGroupsSync | Erstatter delta sync og full sync og synkroniserer kun grupper og Teams. Kræver at skole.azure-ad.teamsAndGroupsOnly er slået til. | 0 10 1 \* \* ? |
