---
title: AD
layout: default
parent: Konfiguration
nav_order: 2
has_children: false
---
# Active Directory integration (on-premise)

| Sti | Beskrivelse | Standardværdi |
| --- | --- | --- |
| JobSettings.FullSyncCron | Cron-udtryk for fuld synkronisering | 0 30 2 \* \* ? \* |
| JobSettings.DeltaSyncCron | Cron-udtryk for delta synkronisering | 0 0/5 \* \* \* ? \* |
| OS2skoledataSettings.BaseUrl | Base URL til OS2skoledata |     |
| OS2skoledataSettings.ApiKey | API-nøgle til OS2skoledata. Der kan via OS2skoledata brugergrænsefladen oprettes en klient med typen "Adgang til API'erne bortset fra import API'et". Hvis der skal håndteres kodeord for indskolingselever, skal typen "Adgang til API'erne inklusiv kodeord på brugere bortset fra import API'et" vælges. |     |
| OS2skoledataSettings.InstitutionWhitelist | Liste over institutioner der må synkroniseres, hvis det ikke er alle institutioner, der anvendes i denne klient. Hvis den efterlades tom, synces alle indlæste institutioner | \[\] |
| OS2skoledataSettings.DryRun | Dry run for OS2skoledata – der sker ingen ændringer i OS2skoledata-core. OS2skoledata rapporterer altså ikke fejl og sætte ikke brugernavn i databasen. | true |
| ActiveDirectorySettings.DisabledUsersOU | OU til deaktiverede brugere |     |
| ActiveDirectorySettings.RootOU | Rod-OU for OS2skoledata |     |
| ActiveDirectorySettings.RootDeletedOusOu | OU til “slettede” OU'er |     |
| ActiveDirectorySettings.KeepAliveOU | OU til brugere der skal holdes aktive, hvis man anvender “forbliv aktiv”-featuren |     |
| ActiveDirectorySettings.OUsToAlwaysCreate | Liste over navne på OU’er der altid skal oprettes under hver institution | \[\] |
| ActiveDirectorySettings.UsersToInclude | Brugere der eksplicit skal medtages. Hvis denne har en værdi, er det kun brugere med disse brugernavne, der håndteres. Bruges til test. | \[\] |
| ActiveDirectorySettings.UsersToIgnore | Brugere der skal ignoreres. Brugere med disse brugernavne håndteres ikke af OS2skoledata | \[\] |
| ActiveDirectorySettings.EmailDomain | Domæne der anvendes til mailadresser |     |
| ActiveDirectorySettings.MoveUsersEnabled | Aktiverer flytning af brugere, hvis true. Er default false, så OS2skoledata ikke flytter burgere før kommunen er klar til det. | false |
| ActiveDirectorySettings.UseUsernameAsKey | Brug brugernavn som identifikator i stedet for cpr | false |
| ActiveDirectorySettings.UsernameKeyField | Krævet, hvis UseUsernameAsKey er true. Felt til hvor brugernavnet, der anvendes til match, står |     |
| ActiveDirectorySettings.UsernameKeyType | Krævet, hvis UseUsernameAsKey er true. Type af brugeridentifikation. SAM_ACCOUNT_NAME eller UNI_ID |     |
| ActiveDirectorySettings.MatchOnSamAccountNameFallbackToCpr | Hvis man matcher på cpr, kan denne indstilling slåes til, så man mathcer på brugernavn, hvis den er der, ellers cpr, som normalt. Det kan fx være nyttigt ved skift af cpr (fiktivt cpr til cpr) | false |
| ActiveDirectorySettings.UseDanishCharacters | Tillad danske tegn i OU- og gruppenavne | false |
| ActiveDirectorySettings.DryRun | Dry run for AD – der sker ingen ændringer i AD, men de ændringer der ville være udført logges. Bruges ofte når man sætter MoveUsersEnabled til true, så brugere rent faktisk ikke flyttes, men flytningen bliver bare simuleret | false |
| ActiveDirectorySettings.CreateOUHierarchy | Opret OU-hierarki automatisk, hvis denne er false, laves der ikke et hirarki og brugerne placeres bare i en specificeret OU | true |
| ActiveDirectorySettings.InstitutionUserOUPath | Udfyldes kun, hvis CreateOUHierarchy = false. Map, der mapper institutionsnummer med den enhed, hvor brugerne skal placeres |     |
| ActiveDirectorySettings.AllSecurityGroupsOU | Udfyldes kun, hvis CreateOUHierarchy = false. OU hvor alle sikkerhedsgrupper skal placeres |     |
| ActiveDirectorySettings.ADFieldForOS2skoledataMark | Udfyldes kun, hvis CreateOUHierarchy = false. OS2skoledata burger dette mærke til at kende de brugere, som den håndtere. Bruges så brugere, der ikke håndteres af OS2skoledata ikke bliver disabled |     |
| ActiveDirectorySettings.MultipleCprExcludedGroupDn | Bruges hvis kommunen fx har samlet det administrative og skolen i samme AD og der derfor er flere brugere med samme cpr nummer. OS2skoledata kan kun håndtere en bruger med et cpr nummer. Så hvis man har flere brugere med samme cpr, skal de brugere, der ikke hører til skolen tilføjes til en gruppe. Stien til den gruppe skrives her. |     |
| ActiveDirectorySettings.DeleteDisabledUsersFully | Aktiver automatisk fuld sletning af brugere. | false |
| ActiveDirectorySettings.DaysBeforeDeletionStudent | Dage før elev slettes efter den er disabled | 60  |
| ActiveDirectorySettings.DaysBeforeDeletionEmployee | Dage før ansat slettes efter den er disabled | 60  |
| ActiveDirectorySettings.DaysBeforeDeletionExternal | Dage før ekstern slettes efter den er disabled | 60  |
| ActiveDirectorySettings.requiredUserFields.CprField | Felt til CPR i AD på en bruger | employeeNumber |
| ActiveDirectorySettings.requiredUserFields.InstitutionNumberField | Felt til institutionsnummer på en bruger | textEncodedORAddress |
| ActiveDirectorySettings.optionalUserFields.InstitutionNameField | Felt for institutionsnavn (valgfrit)  <br>Skal være et felt, der kan indeholde mange tegn, da det bliver langt, hvis brugeren er tilknyttet mange institutioner<br><br>kommasepareret |     |
| ActiveDirectorySettings.optionalUserFields.InstitutionAbbreviationField | Felt for insitutions-forkortelse ( valgfrit). Kommasepareret, og kan potentielt blive et langt felt, hvis brugeren er tiknyttet mange institutioner |     |
| ActiveDirectorySettings.optionalUserFields.UNIIdField | Felt for UNI-ID (valgfrit) |     |
| ActiveDirectorySettings.optionalUserFields.MailField | Felt for mailadresse (valgfrit) |     |
| ActiveDirectorySettings.optionalUserFields.STILRolesField | Felt for STIL-roller (valgfrit)  <br>Alle STIL-roller kommasepareret |     |
| ActiveDirectorySettings.optionalUserFields.IgnoreField | Felt brugt til at ignorere bruger (valgfrit)  <br>Hvis der står noget som helst i dette felt på brugeren, ignoreres brugeren af OS2skoledata |     |
| ActiveDirectorySettings.optionalUserFields.StudentStartYearField | Felt for elevens startår (valgfrit)  <br>Baseret på enheden, som brugeren er placeret i |     |
| ActiveDirectorySettings.optionalUserFields.CurrentInstitutionField | Felt for nuværende institution (valgfrit)  <br>Institutionsnavn baseret på enheden, som brugeren er placeret i |     |
| ActiveDirectorySettings.optionalUserFields.GlobalRoleField | Felt for global rolle (valgfrit, men krævet hvis automatisk sletning)  <br>Indeholder den højeste rolle brugeren har – EMPLOYEE, EXTERNAL eller STUDENT |     |
| ActiveDirectorySettings.optionalUserFields.DisabledDateField | Felt for deaktiveringsdato (valgfrit, men krævet hvis automatisk sletning) |     |
| ActiveDirectorySettings.requiredOUFields.OUIdField | Felt til OS2skoledatas genererede ID på en OU | wWWHomePage |
| ActiveDirectorySettings.requiredSecurityGroupFields.SecurityGroupIdField | Felt til OS2skoledatas genererede ID på en sikkerhedsgruppe | wWWHomePage |
| ActiveDirectorySettings.requiredSecurityGroupFields.InstitutionNumberField | Institutionsnummerfelt for gruppe | textEncodedORAddress |
| ActiveDirectorySettings.OptionalSecurityGroupFields.SetSamAccountName | Tilføj samAccountName til grupper ellers danner AD et samAccountName automatisk | false |
| ActiveDirectorySettings.OptionalSecurityGroupFields.SamAccountPrefix | Prefix til samAccountName  <br>Anvendes for at sikre at gruppernes samAccountName ikke konflikter med tidligere gruppers | OS2 |
| ActiveDirectorySettings.OptionalSecurityGroupFields.SamAccountUseInstitutionType | Brug institutionstype til navngivning<br><br>Anvendes hvis der er skoler og daginstitutioner med samme navn | false |
| ActiveDirectorySettings.OptionalSecurityGroupFields.MailField | Mailfelt for grupper (valgfrit) |     |
| ActiveDirectorySettings.OptionalSecurityGroupFields.MailDomain | Krævet, hvis MailField er udfyldt<br><br>Maildomæne for grupper |     |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OverwriteExistingMail | Tillad at eksisterende værdi i MailField overskrives | true |
| ActiveDirectorySettings.OptionalSecurityGroupFields.NormalMailNameStandard | Krævet, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails | {INSTITUTION_NAME}-{CLASS_YEAR}-{CLASS_LINE}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.NoLineNameStandard | Krævet, hvis MailField er udfyldt<br><br>Samme som ovenstående, men bruges hvis gruppen ikke har en linje (fx A)<br><br>Anvendes ofte, hvis der ikke er tale om en skoleklasse | {INSTITUTION_NAME}-{CLASS_YEAR}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.NoLineNoYearNameStandard | Krævet, hvis MailField er udfyldt<br><br>Samme som ovenstående, men bruges hvis gruppen ikke har en linje eller et start år (fx A 2024)<br><br>Anvendes ofte, hvis der ikke er tale om en skoleklasse | {INSTITUTION_NAME}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.SecurityGroupForEmployeesMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med med medarbejdere for institutionerne| {INSTITUTION_NAME}-alle-medarbejdere@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.SecurityGroupForEmployeeTypeMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med bestemte medarbejder typer | {INSTITUTION_NAME}-type-{TYPE}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OtherGroupsÅrgangSecurityGroupMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med typen årgang | {INSTITUTION_NAME}-Årgang-{DATABASE_ID}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OtherGroupsRetningSecurityGroupMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med typen retming | {INSTITUTION_NAME}-Retning-{DATABASE_ID}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OtherGroupsHoldSecurityGroupMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med typen hold | {INSTITUTION_NAME}-Hold-{DATABASE_ID}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OtherGroupsSFOSecurityGroupMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med typen SFO | {INSTITUTION_NAME}-SFO-{DATABASE_ID}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OtherGroupsTeamSecurityGroupMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med typen team | {INSTITUTION_NAME}-Team-{DATABASE_ID}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.OptionalSecurityGroupFields.OtherGroupsAndetSecurityGroupMailStandard | mulig, hvis MailField er udfyldt<br><br>Navnestandard for gruppe-mails til grupperne med typen andet | {INSTITUTION_NAME}-Andet-{DATABASE_ID}-{CLASS_NAME}@{DOMAIN} |
| ActiveDirectorySettings.usernameSettings.UsernameStandard | Strategi til opbygning af brugernavne for nye brugere. Se sektion omkring brugernavnestandarder. | FROM_STIL_OR_AS_UNILOGIN_RANDOM |
| ActiveDirectorySettings.usernameSettings.UsernamePrefix | Præfiks til brugernavne, hvis brugernavnestandarden understøtter det |     |
| ActiveDirectorySettings.usernameSettings.RandomStandardLetterCount | Antal bogstaver brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| ActiveDirectorySettings.usernameSettings.RandomStandardNumberCount | Antal tal I brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| ActiveDirectorySettings.filteringSettings.GloballyExcludedRoles | Roller der altid ekskluderes | \[ "BARN" \] |
| ActiveDirectorySettings.filteringSettings.ExludedRolesInInstitution | Roller ekskluderet pr. institution |     |
| ActiveDirectorySettings.namingSettings.EmployeeOUName | Navn til enheden under hver institution til medarbejdere | medarbejdere |
| ActiveDirectorySettings.namingSettings.StudentOUName | Navn til enheden under hver institution til elever | elever |
| ActiveDirectorySettings.namingSettings.StudentsWithoutGroupsOUName | Navn til enheden under hver institution til elever uden grupper | elever udenfor grupper |
| ActiveDirectorySettings.namingSettings.SecurityGroupOUName | Navn til enheden under hver institution til sikkerhedsgrupper | sikkerhedsgrupper |
| ActiveDirectorySettings.namingSettings.ClassOUNameStandard | Navnestandard for klasse OU | {CLASS_NAME}\_{CLASS_YEAR} |
| ActiveDirectorySettings.namingSettings.ClassOUNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.InstitutionOUNameStandard | Navnestandard for Institutions OU | {INSTITUTION_NAME} ({INSTITUTION_NUMBER}) |
| ActiveDirectorySettings.namingSettings.AllInInstitutionSecurityGroupNameStandard | Navnestandard for gruppe til alle i en institution | {INSTITUTION_NAME}\_alle |
| ActiveDirectorySettings.namingSettings.AllStudentsInInstitutionSecurityGroupNameStandard | Navnestandard for gruppe til alle elever i en institution | {INSTITUTION_NAME}\_elever |
| ActiveDirectorySettings.namingSettings.AllEmployeesInInstitutionSecurityGroupNameStandard | Navnestandard for gruppe til alle ansatte i en institution | {INSTITUTION_NAME}\_medarbejdere |
| ActiveDirectorySettings.namingSettings.ClassSecurityGroupNameStandard | Navnestandard for klassegruppe med år/linje | {CLASS_NAME}\_{CLASS_YEAR}\_alle |
| ActiveDirectorySettings.namingSettings.ClassSecurityGroupNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {CLASS_NAME}\_alle |
| ActiveDirectorySettings.namingSettings.ClassStudentsSecurityGroupNameStandard | Navnestandard for klassegruppe kun med elever med år/linje | {CLASS_NAME}\_{CLASS_YEAR}\_elever |
| ActiveDirectorySettings.namingSettings.ClassStudentsSecurityGroupNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {CLASS_NAME}\_elever |
| ActiveDirectorySettings.namingSettings.ClassEmployeesSecurityGroupNameStandard | Navnestandard for klassegruppe kun med medarbejdere med år/linje | {CLASS_NAME}\_{CLASS_YEAR}\_medarbejdere |
| ActiveDirectorySettings.namingSettings.ClassEmployeesSecurityGroupNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {CLASS_NAME}\_medarbejdere |
| ActiveDirectorySettings.namingSettings.OtherGroupsÅrgangSecurityGroupNameStandard | Navnestandard for sikkerhedsgrupper til grupper fra STIL af typen årgang | Årgang_{DATABASE_ID}_{CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.OtherGroupsRetningSecurityGroupNameStandard | Navnestandard for sikkerhedsgrupper til grupper fra STIL af typen retning | Retning_{DATABASE_ID}_{CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.OtherGroupsHoldSecurityGroupNameStandard | Navnestandard for sikkerhedsgrupper til grupper fra STIL af typen hold | Hold_{DATABASE_ID}_{CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.OtherGroupsSFOSecurityGroupNameStandard | Navnestandard for sikkerhedsgrupper til grupper fra STIL af typen SFO | SFO_{DATABASE_ID}_{CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.OtherGroupsTeamSecurityGroupNameStandard | Navnestandard for sikkerhedsgrupper til grupper fra STIL af typen team | Team_{DATABASE_ID}_{CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.OtherGroupsAndetSecurityGroupNameStandard | Navnestandard for sikkerhedsgrupper til grupper fra STIL af typen andet | Andet_{DATABASE_ID}_{CLASS_NAME} |
| ActiveDirectorySettings.namingSettings.SecurityGroupForEmployeeTypeNameStandard | Navnestandard for gruppe for medarbejdertype | {INSTITUTION_NAME}type{TYPE}\_alle |
| ActiveDirectorySettings.namingSettings.SecurityGroupForYearNameStandard | Navnestandard for gruppe for årgang | {INSTITUTION_NAME}elever_år{YEAR} |
| ActiveDirectorySettings.namingSettings.SecurityGroupForLevelNameStandard | Navnestandard for gruppe til klassetrin | {INSTITUTION_NAME} {LEVEL}. klasse |
| ActiveDirectorySettings.namingSettings.GlobalStudentSecurityGroupName | Navn på global elevgruppe | alle_elever |
| ActiveDirectorySettings.namingSettings.GlobalEmployeeSecurityGroupName | Navn på global medarbejdergruppe | alle_medarbejdere |
| ActiveDirectorySettings.namingSettings.GlobalSecurityGroupForEmployeeTypeSchoolNameStandard | Navnestandard for global gruppe pr medarbejdertype – skoler | alle_{TYPE}\_skoler |
| ActiveDirectorySettings.namingSettings.GlobalSecurityGroupForEmployeeTypeDaycareNameStandard | Navnestandard for global gruppe pr medarbejdertype – daginstitutioner | alle_{TYPE}\_daginstitutioner |
| ActiveDirectorySettings.namingSettings.GlobalSecurityGroupForEmployeeTypeFUNameStandard | Navnestandard for global gruppe pr medarbejdertype – FU | alle_{TYPE}\_fu |
| ActiveDirectorySettings.namingSettings.GlobalSecurityGroupForLevelNameStandard | Navnestandard for global gruppe for klassetrin | {LEVEL}. klasse |
| ActiveDirectorySettings.namingSettings.SchoolOUName | Navn på OU for typen skoler | Skoler |
| ActiveDirectorySettings.namingSettings.DaycareOUName | Navn på OU for typen daginstitutioner | Daginstitutioner |
| ActiveDirectorySettings.namingSettings.FuOUName | Navn på OU for typen FU | FU  |
| ActiveDirectorySettings.StudentAndClassGroupsSchoolsOnly | hvis true, vil der kun blive oprettet elev og klassegrupper til institutioner af typen skole |false   |
| PowerShellSettings.createPowerShellScript | Sti til powershell script der køres efter oprettelse eller reaktivering af brugere | C:\\Program Files (x86)\\Digital Identity\\OS2skoledataADSync\\PowerShell\\createUser.ps1 |
| PowerShellSettings.DisablePowerShellScript | Sti til powershell script der køres efter deaktivering af brugere | C:\\Program Files (x86)\\Digital Identity\\OS2skoledataADSync\\PowerShell\\disableUser.ps1 |
| PowerShellSettings.DryRun | Dry run for PowerShell – hvis true, køres der ikke powershell | true |
| PowerShellSettings.UserAsJSON | Send hele brugerobjektet i JSON til powershell scriptet som parameter | false |
| PAMSettings.Enabled | Aktiver hentning af API key fra CyberArk | false |
| PAMSettings.CyberArkAppId | CyberArk app id |     |
| PAMSettings.CyberArkSafe | CyberArk kode |     |
| PAMSettings.CyberArkObject | CyberArk object |     |
| PAMSettings.CyberArkAPI | CyberArk URL |     |
| LogUploaderSettings.Enabled | Aktiver upload af logs til S3, så Digital Identity kan tilgå dem | false |
| LogUploaderSettings.FileShareUrl | URL til S3 fileshare | [https://s3fileshare.digital-identity.dk](https://s3fileshare.digital-identity.dk/) |
| LogUploaderSettings.FileShareApiKey | API-nøgle til S3 fileshare | ""  |
