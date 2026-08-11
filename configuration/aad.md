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
| <span id="skole.azure-ad.clientID">skole.azure-ad.clientID</span> | Klient-ID for Azure AD-applikationen. |     |
| <span id="skole.azure-ad.clientSecret">skole.azure-ad.clientSecret</span> | Klienthemmelighed til Azure AD-applikationen. |     |
| <span id="skole.azure-ad.usingPEMCertificate">skole.azure-ad.usingPEMCertificate</span> | Brug PEM certifikat for adgang til Azure. Kræver udfyldning af skole.azure-ad.certificatePath | false |
| <span id="skole.azure-ad.certificatePath">skole.azure-ad.certificatePath</span> | Bruges kun hvis skole.azure-ad.usingPEMCertificate er ”true”. Ruten til PEM certifikatet. |     |
| <span id="skole.azure-ad.tenantID">skole.azure-ad.tenantID</span> | Tenant-ID for Azure AD. |     |
| <span id="skole.azure-ad.userDryRun">skole.azure-ad.userDryRun</span> | Opret grupper og teams uden at udføre handlinger med brugere. | false |
| <span id="skole.azure-ad.teamsAndGroupsOnly">skole.azure-ad.teamsAndGroupsOnly</span> | Synkroniser kun teams og grupper – håndter ikke brugere | false |
| <span id="skole.os2skoledata.apiKey">skole.os2skoledata.apiKey</span> | API-nøgle til OS2skoledata. Der kan via OS2skoledata brugergrænsefladen oprettes en klient med typen "Adgang til API'erne bortset fra import API'et". Hvis der skal håndteres kodeord for indskolingselever, skal typen "Adgang til API'erne inklusiv kodeord på brugere bortset fra import API'et" vælges.|     |
| <span id="skole.os2skoledata.baseUrl">skole.os2skoledata.baseUrl</span> | URL til OS2skoledata API. |     |
| <span id="skole.syncSettings.domain">skole.syncSettings.domain</span> | Domæne – bruges fx til email |     |
| <span id="skole.syncSettings.useUsernameAsKey">skole.syncSettings.useUsernameAsKey</span> | Brug brugernavn som nøgle I stedet for cpr | false |
| <span id="skole.syncSettings.uniIdField">skole.syncSettings.uniIdField</span> | Felt på burgere i Azure AD til Uni-login. Mulige:  <br>NONE, DEPARTMENT, EMPLOYEE_ID | NONE |
| <span id="skole.syncSettings.usernameSettings.usernameStandard">skole.syncSettings.usernameSettings.usernameStandard</span> | Strategi til opbygning af brugernavne for nye brugere. Se sektion omkring brugernavnestandarder. |     |
| <span id="skole.syncSettings.usernameSettings.usernamePrefix">skole.syncSettings.usernameSettings.usernamePrefix</span> | Præfiks til brugernavne, hvis brugernavnestandarden understøtter det |     |
| <span id="skole.syncSettings.usernameSettings.randomStandardLetterCount">skole.syncSettings.usernameSettings.randomStandardLetterCount</span> | Antal bogstaver brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| <span id="skole.syncSettings.usernameSettings.randomStandardNumberCount">skole.syncSettings.usernameSettings.randomStandardNumberCount</span> | Antal tal I brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| <span id="skole.syncSettings.filteringSettings.globallyExcludedRoles">skole.syncSettings.filteringSettings.globallyExcludedRoles</span> | Roller der altid ekskluderes fra oprettelse | \[\] |
| <span id="skole.syncSettings.filteringSettings.exludedRolesInInstitution">skole.syncSettings.filteringSettings.exludedRolesInInstitution</span> | Institutionsspecifik eksklusion. | {}  |
| <span id="skole.syncSettings.nameStandards.allInInstitutionSecurityGroupNameStandard">skole.syncSettings.nameStandards.allInInstitutionSecurityGroupNameStandard</span> | Navnestandard for sikkerhedsgruppen for alle brugere i institutionen. |     |
| <span id="skole.syncSettings.nameStandards.allStudentsInInstitutionSecurityGroupNameStandard">skole.syncSettings.nameStandards.allStudentsInInstitutionSecurityGroupNameStandard</span> | Navnestandard for sikkerhedsgruppen for alle elever i institutionen. |     |
| <span id="skole.syncSettings.nameStandards.allEmployeesInInstitutionSecurityGroupNameStandard">skole.syncSettings.nameStandards.allEmployeesInInstitutionSecurityGroupNameStandard</span> | Navnestandard for sikkerhedsgruppen for alle medarbejdere i institutionen. |     |
| <span id="skole.syncSettings.nameStandards.classSecurityGroupNameStandard">skole.syncSettings.nameStandards.classSecurityGroupNameStandard</span> | Navnestandard for sikkerhedsgruppen for alle i en klasse |     |
| <span id="skole.syncSettings.nameStandards.classSecurityGroupNameStandardNoClassYear">skole.syncSettings.nameStandards.classSecurityGroupNameStandardNoClassYear</span> | Navnestandard for ovenstående gruppe, der anvendes hvis klassen ikke har startår |     |
| <span id="skole.syncSettings.nameStandards.globalEmployeeSecurityGroupName">skole.syncSettings.nameStandards.globalEmployeeSecurityGroupName</span> | Navnestandard for global medarbejdergruppe. |     |
| <span id="skole.syncSettings.nameStandards.globalStudentSecurityGroupName">skole.syncSettings.nameStandards.globalStudentSecurityGroupName</span> | Navnestandard for global elevgruppe. |     |
| <span id="skole.syncSettings.nameStandards.allEmployeesInInstitutionTeamNameStandard">skole.syncSettings.nameStandards.allEmployeesInInstitutionTeamNameStandard</span> | Navnestandard for team for ansatte. |     |
| <span id="skole.syncSettings.nameStandards.allEmployeesInInstitutionTeamMailStandard">skole.syncSettings.nameStandards.allEmployeesInInstitutionTeamMailStandard</span> | Navnestandard for mail til team med ansatte. |     |
| <span id="skole.syncSettings.nameStandards.classTeamNameStandard">skole.syncSettings.nameStandards.classTeamNameStandard</span> | Navnestandard for team for klasse. |     |
| <span id="skole.syncSettings.nameStandards.classTeamNameStandardNoClassYear">skole.syncSettings.nameStandards.classTeamNameStandardNoClassYear</span> | Navnestandard for ovenstående team, der anvendes hvis klassen ikke har startår |     |
| <span id="skole.syncSettings.nameStandards.classTeamMailStandard">skole.syncSettings.nameStandards.classTeamMailStandard</span> | Navnestandard for mail til klasseteam. |     |
| <span id="skole.syncSettings.nameStandards.classTeamMailStandardNoClassYear">skole.syncSettings.nameStandards.classTeamMailStandardNoClassYear</span> | Navnestandard for mail til ovenstående team, der anvendes hvis klassen ikke har startår |     |
| <span id="skole.syncSettings.nameStandards.levelSecurityGroupNameStandard">skole.syncSettings.nameStandards.levelSecurityGroupNameStandard</span> | Navnestandard for klassetrin-gruppe |     |
| <span id="skole.syncSettings.nameStandards.globalLevelSecurityGroupNameStandard">skole.syncSettings.nameStandards.globalLevelSecurityGroupNameStandard</span> | Navnestandard for global klassetring-gruppe |     |
| <span id="skole.syncSettings.azureTeamsSettings.handleTeams">skole.syncSettings.azureTeamsSettings.handleTeams</span> | Aktiverer synkronisering af Teams | false |
| <span id="skole.syncSettings.azureTeamsSettings.readOnlyPeriod">skole.syncSettings.azureTeamsSettings.readOnlyPeriod</span> | Antal dage et team skal være skrivebeskyttet inden det slettes | 90  |
| <span id="skole.syncSettings.azureTeamsSettings.classTeamTemplate">skole.syncSettings.azureTeamsSettings.classTeamTemplate</span> | Navn på Team-skabelon for klasser. | educationClass |
| <span id="skole.syncSettings.azureTeamsSettings.employeeTeamTemplate">skole.syncSettings.azureTeamsSettings.employeeTeamTemplate</span> | Navn på Team-skabelon for ansatte. | standard |
| <span id="skole.syncSettings.deleteUserSettings.enabled">skole.syncSettings.deleteUserSettings.enabled</span> | Aktiver automatisk fuld sletning af brugere. | false |
| <span id="skole.syncSettings.deleteUserSettings.daysBeforeDeletionStudent">skole.syncSettings.deleteUserSettings.daysBeforeDeletionStudent</span> | Dage før elev slettes efter den er disabled | 60  |
| <span id="skole.syncSettings.deleteUserSettings.daysBeforeDeletionEmployee">skole.syncSettings.deleteUserSettings.daysBeforeDeletionEmployee</span> | Dage før ansat slettes efter den er disabled | 60  |
| <span id="skole.syncSettings.deleteUserSettings.daysBeforeDeletionExternal">skole.syncSettings.deleteUserSettings.daysBeforeDeletionExternal</span> | Dage før ekstern slettes efter den er disabled | 60  |
| <span id="cron.deltaSync">cron.deltaSync</span> | Cron udtryk for hvornår der skal køres delta sync | 0 0/5 \* \* \* ? |
| <span id="cron.fullSync">cron.fullSync</span> | Cron udtryk for hvornår der skal køres fuld sync | 0 10 1 \* \* ? |
| <span id="cron.teamsAndGroupsSync">cron.teamsAndGroupsSync</span> | Erstatter delta sync og full sync og synkroniserer kun grupper og Teams. Kræver at skole.azure-ad.teamsAndGroupsOnly er slået til. | 0 10 1 \* \* ? |
