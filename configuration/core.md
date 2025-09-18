---
title: Core
layout: default
parent: Konfiguration
nav_order: 1
has_children: false
---
# OS2skoledata core

| Sti | Beskrivelse | Standardværdi |
| --- | --- | --- |
| os2skoledata.dev | Aktiverer udviklingstilstand | false |
| os2skoledata.ignoreNameProtection | Ignorerer navnebeskyttelse | false |
| os2skoledata.ignoreNameProtectionEmployeesOnly | Ignorerer navnebeskyttelse for medarbejdere og eksterne | false |
| os2skoledata.stilUsername | Brugernavn til STIL-login. |     |
| os2skoledata.stilPassword | Adgangskode til STIL-login. |     |
| os2skoledata.institutions | Liste over institutioner der synkroniseres. Institutionsnummer, type og evt en unik forkortelse | \[\] |
| os2skoledata.studentAdministration.enabled | Aktiverer administration af elevers kodeord og klasselister | false |
| os2skoledata.studentAdministration.classListsOnly | Gør det muligt at kunne tilgå klasselister, men slår kodeordsfunktionalitet fra. Kræver os2skoledata.studentAdministration.enabled = true | false |
| os2skoledata.studentAdministration.passwordSecret | Hemmelighed brugt til at danne adgangskoder. |     |
| os2skoledata.studentAdministration.parentPasswordChangeEnabled | Tillader forældre at ændre adgangskoder på deres egne børn | false |
| os2skoledata.studentAdministration.indskolingSpecialEnabled | Viser særligt skærmbillede, når der skal skiftes kodeord på elever i indskolingen. Her vælges to nemme ord og et tal | false |
| os2skoledata.studentAdministration.setIndskolingPasswordOnCreate | Sætter adgangskode automatisk ved nyoprettelse af indskolingselever i klienterne. | false |
| os2skoledata.cpr.enabled | Aktiverer opslag i CPR-service.<br><br>Denne bruges, hvis forældre logger ind, til at se hvilke elever, de må skifte kodeord på. | true |
| os2skoledata.cpr.url | URL til CPR-tjenesten. | [http://cprservice5.digital-identity.dk](http://cprservice5.digital-identity.dk/) |
| os2skoledata.cvr | Kommunens CVR-nummer. |     |
| os2skoledata.idp.employee | IDP-konfiguration for ansatte. Metadata og entityId. | {}  |
| os2skoledata.idp.parent | IDP-konfiguration for forældre. Metadata og entityId. | {}  |
| os2skoledata.teamAdminAdministration.enabled | Aktiverer administration af teams. | false |
| os2skoledata.ghostAdministration.enabled | Aktiverer understøttelse af brugere, der skal forblive aktive selvom de ikke længere er i STIL |     |
| os2skoledata.email.from | Afsenderadresse for e-mails sendt fra systemet. |     |
| os2skoledata.email.username | Brugernavn til e-mail server. |     |
| os2skoledata.email.password | Adgangskode til e-mail server. |     |
| os2skoledata.email.host | E-mailserverens hostnavn. |     |
| os2skoledata.deleteInstitutionPersonAfterMonths | Måneder før person slettes i databasen efter den ikke længere er i STIL. | 13  |
| os2skoledata.deleteAuditLogsAfterMonths | Måneder før AuditLogs slettes i databasen. | 13  |
| os2skoledata.filterOutGroupsWithFutureFromDate | Filtrér grupper med level 0 fra med fremtidig startdato. Det er kun level 0, der filtreres fra, da det ellers vil give problemer ved årsrul | false |
| os2skoledata.createGroupsXDaysBeforeFromDate | Dage før gruppens startdato den skal oprettes i klienterne. Hører sammen med indstillingen ovenfor. | 60  |
| os2skoledata.classroomAdministration.enabled | Aktiverer understøttelse af overdragelse og arkivering af Google Classrooms. | false |
| os2skoledata.scheduled.enabled | Aktiverer planlagt synkronisering. | false |
| os2skoledata.scheduled.modificationHistoryCleanup.days | Hvor mange dage der skal gemmes ændringshistorik fra | 90  |
| os2skoledata.scheduled.cron | Cron udtryk for hvornår der skal hentes data fra STIL. Som standard en gang om dagen. Kan ændres til op til fire gange om dagen. |     |
| os2skoledata.syncSettings.syncFrom | Beskriver hvorfra der loades data ind i OS2skoledata. Mulige værdier: STIL, API_AND_STIL | STIL |
| os2skoledata.syncSettings.fieldsMaintainedBySTIL | Udfyldes kun hvis syncFrom er API_AND_STIL. Beskriver hvilke felter, der vedligeholdes af STIL. De resterende er vedligeholdt via API. Mulige værdier:  <br>UNI_LOGIN,<br><br>GROUP_IDS,<br><br>NAME_PROTECTED,<br><br>ALIAS_FIRST_NAME,<br><br>ALIAS_FAMILY_NAME | \[\] |
| os2skoledata.syncSettings. transitionMode | Kan sættes hvis syncFrom er API_AND_STIL.  <br>Hvis syncFrom er API_AND_STIL, tillader vi normalt ikke, at STIL opretter og sletter brugere,<br><br>men det kan være nødvendigt ved den første indlæsning eller under en testperiode, når kommunen implementerer mod import-API'et.<br><br>Hvis transitionMode er true, tillader vi, at STIL opretter alle brugere og sletter brugere, hvor source er forskellig fra localSource. Ingen opdateringer. | false |
| os2skoledata.syncSettings.localSource | Den source der normal sættes på brugere indlæst via indlæsnings-API’et. Bruges så til at sikre at vi ikke sletter brugere fra localSource hvis transitionMode er true. | local |
| os2skoledata.syncSettings.onlySaveNeededPropertiesFromSTIL | Gemmer kun felter fra STIL i databasen, som bruges af OS2skoledata. Det vil sige at fx kontaktpersoner og adresser ikke gemmes, hvis denne indstilling sættes til true. | false |
| os2skoledata.syncSettings.thresholdPercentage | Den procentsats i decimal tal, der skal til før en ændring i antallet af personer tilknyttet en institution, registreres som en stor ændring. | 0.5 (50%) |