---
title: GW
layout: default
parent: Konfiguration
nav_order: 3
has_children: false
---
# Google Workspace integration

| Sti | Beskrivelse | Standardværdi |
| --- | --- | --- |
| <span id="JobSettings.FullSyncCron">JobSettings.FullSyncCron</span> | Cron-udtryk for fuld synkronisering | 0 43 2 \* \* ? \* |
| <span id="JobSettings.DeltaSyncCron">JobSettings.DeltaSyncCron</span> | Cron-udtryk for delta-synkronisering | 0 0/5 \* \* \* ? \* |
| <span id="JobSettings.ClassroomSyncCron">JobSettings.ClassroomSyncCron</span> | Cron-udtryk for Classroom-synkronisering, hvis det er slået til | 0 3/5 \* \* \* ? \* |
| <span id="OS2skoledataSettings.BaseUrl">OS2skoledataSettings.BaseUrl</span> | Base URL til OS2skoledata API |     |
| <span id="OS2skoledataSettings.ApiKey">OS2skoledataSettings.ApiKey</span> | API-nøgle til OS2skoledata. Der kan via OS2skoledata brugergrænsefladen oprettes en klient med typen "Adgang til API'erne bortset fra import API'et". Hvis der skal håndteres kodeord for indskolingselever, skal typen "Adgang til API'erne inklusiv kodeord på brugere bortset fra import API'et" vælges. |     |
| <span id="WorkspaceSettings.ServiceAccountDataFilePath">WorkspaceSettings.ServiceAccountDataFilePath</span> | Filsti til servicekonto JSON-fil |     |
| <span id="WorkspaceSettings.EmailAccountToImpersonate">WorkspaceSettings.EmailAccountToImpersonate</span> | Konto der skal impersoneres i Google |     |
| <span id="WorkspaceSettings.Domain">WorkspaceSettings.Domain</span> | Domæne for Google Workspace |     |
| <span id="WorkspaceSettings.RootOrgUnitPath">WorkspaceSettings.RootOrgUnitPath</span> | Rod-OU til oprettelse af underenheder | /OS2skoledata |
| <span id="WorkspaceSettings.OUsToAlwaysCreate">WorkspaceSettings.OUsToAlwaysCreate</span> | Liste over OU'er der altid skal oprettes | \[\] |
| <span id="WorkspaceSettings.SuspendedUsersOU">WorkspaceSettings.SuspendedUsersOU</span> | OU til suspenderede brugere | /OS2skoledata/Suspended |
| <span id="WorkspaceSettings.DeletedOusOu">WorkspaceSettings.DeletedOusOu</span> | OU til “slettede” enheder | /OS2skoledata/Suspended |
| <span id="WorkspaceSettings.KeepAliveOU">WorkspaceSettings.KeepAliveOU</span> | OU til brugere der skal holdes aktive, hvis man anvender “forbliv aktiv”-featuren | /OS2skoledata/keepalive |
| <span id="WorkspaceSettings.HierarchyType">WorkspaceSettings.HierarchyType</span> | Strukturtype for OU-hierarki | INSTITUTION_FIRST |
| <span id="WorkspaceSettings.NamingSettings.EmployeeOUName">WorkspaceSettings.NamingSettings.EmployeeOUName</span> | Navn på medarbejder-OU | Medarbejdere |
| <span id="WorkspaceSettings.NamingSettings.StudentOUName">WorkspaceSettings.NamingSettings.StudentOUName</span> | Navn på elev-OU | Elever |
| <span id="WorkspaceSettings.NamingSettings.StudentsWithoutGroupsOUName">WorkspaceSettings.NamingSettings.StudentsWithoutGroupsOUName</span> | Navn på OU for elever uden grupper (oprettes under hver institution) | Elever udenfor grupper |
| <span id="WorkspaceSettings.NamingSettings.ClassOUNameStandard">WorkspaceSettings.NamingSettings.ClassOUNameStandard</span> | Navnestandard for klasse-OU | {CLASS_NAME} |
| <span id="WorkspaceSettings.NamingSettings.ClassOUNameStandardNoClassYear">WorkspaceSettings.NamingSettings.ClassOUNameStandardNoClassYear</span> | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {CLASS_NAME} |
| <span id="WorkspaceSettings.NamingSettings.InstitutionOUNameStandard">WorkspaceSettings.NamingSettings.InstitutionOUNameStandard</span> | Navnestandard for institution-OU | {INSTITUTION_NAME} ({INSTITUTION_NUMBER}) |
| <span id="WorkspaceSettings.NamingSettings.AllEmployeesInInstitutionDriveNameStandard">WorkspaceSettings.NamingSettings.AllEmployeesInInstitutionDriveNameStandard</span> | Navnestandard for drev til alle medarbejdere på en institution | {INSTITUTION_NAME} - medarbejdere |
| <span id="WorkspaceSettings.NamingSettings.ClassDriveNameStandard">WorkspaceSettings.NamingSettings.ClassDriveNameStandard</span> | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME} {CLASS_NAME} - alle |
| <span id="WorkspaceSettings.NamingSettings.ClassDriveNameStandardNoClassYear">WorkspaceSettings.NamingSettings.ClassDriveNameStandardNoClassYear</span> | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME} {CLASS_NAME} - alle |
| <span id="WorkspaceSettings.NamingSettings.GlobalEmployeeDriveName">WorkspaceSettings.NamingSettings.GlobalEmployeeDriveName</span> | Navn på globalt medarbejderdrev | Alle medarbejdere |
| <span id="WorkspaceSettings.NamingSettings.DeletedDrivePrefix">WorkspaceSettings.NamingSettings.DeletedDrivePrefix</span> | Prefix for “slettede” drev | Slettet_ |
| <span id="WorkspaceSettings.NamingSettings.AllInInstitutionGroupNameStandard">WorkspaceSettings.NamingSettings.AllInInstitutionGroupNameStandard</span> | Navnestandard for gruppe for alle i en institution | {INSTITUTION_NAME} - alle |
| <span id="WorkspaceSettings.NamingSettings.AllStudentsInInstitutionGroupNameStandard">WorkspaceSettings.NamingSettings.AllStudentsInInstitutionGroupNameStandard</span> | Navnestandard for gruppe for alle elever i en institution | {INSTITUTION_NAME} - elever |
| <span id="WorkspaceSettings.NamingSettings.AllEmployeesInInstitutionGroupNameStandard">WorkspaceSettings.NamingSettings.AllEmployeesInInstitutionGroupNameStandard</span> | Navnestandard for gruppe for alle medarbejdere i en institution | {INSTITUTION_NAME} - medarbejdere |
| <span id="WorkspaceSettings.NamingSettings.GroupForEmployeeTypeNameStandard">WorkspaceSettings.NamingSettings.GroupForEmployeeTypeNameStandard</span> | Navnestandard for gruppe for medarbejdertype | {INSTITUTION_NAME} - alle - {TYPE} |
| <span id="WorkspaceSettings.NamingSettings.GroupForYearNameStandard">WorkspaceSettings.NamingSettings.GroupForYearNameStandard</span> | Navnestandard for årgangsgruppe | {INSTITUTION_NAME} - elever - {YEAR} |
| <span id="WorkspaceSettings.NamingSettings.ClassGroupNameStandard">WorkspaceSettings.NamingSettings.ClassGroupNameStandard</span> | Navnestandard for klassegruppe | {INSTITUTION_NAME}-{CLASS_NAME}-{CLASS_YEAR} - alle |
| <span id="WorkspaceSettings.NamingSettings.ClassGroupNameStandardNoClassYear">WorkspaceSettings.NamingSettings.ClassGroupNameStandardNoClassYear</span> | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME}-{CLASS_NAME} - alle |
| <span id="WorkspaceSettings.NamingSettings.ClassGroupOnlyStudentsNameStandard">WorkspaceSettings.NamingSettings.ClassGroupOnlyStudentsNameStandard</span> | Navnestandard for gruppe kun for elever | {INSTITUTION_NAME}-{CLASS_NAME}-{CLASS_YEAR} - elever |
| <span id="WorkspaceSettings.NamingSettings.ClassGroupOnlyStudentsNameStandardNoClassYear">WorkspaceSettings.NamingSettings.ClassGroupOnlyStudentsNameStandardNoClassYear</span> | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME}-{CLASS_NAME} - elever |
| <span id="WorkspaceSettings.NamingSettings.GlobalEmployeeGroupName">WorkspaceSettings.NamingSettings.GlobalEmployeeGroupName</span> | Navn på global medarbejdergruppe | Alle medarbejdere |
| <span id="WorkspaceSettings.NamingSettings.SchoolOUName">WorkspaceSettings.NamingSettings.SchoolOUName</span> | Navn på OU til skoler | Skoler |
| <span id="WorkspaceSettings.NamingSettings.DaycareOUName">WorkspaceSettings.NamingSettings.DaycareOUName</span> | Navn på OU til dagtilbud | Dagtilbud |
| <span id="WorkspaceSettings.NamingSettings.FuOUName">WorkspaceSettings.NamingSettings.FuOUName</span> | Navn på OU for typen FU | FU  |
| <span id="WorkspaceSettings.NamingSettings.InstitutitonStaffGroupEmailTypeName">WorkspaceSettings.NamingSettings.InstitutitonStaffGroupEmailTypeName</span> | Ord, der bruges i mail til medarbejdergruppe | staff |
| <span id="WorkspaceSettings.NamingSettings.OnlyUseYearInClassGroupEmail">WorkspaceSettings.NamingSettings.OnlyUseYearInClassGroupEmail</span> | Brug kun årstal i mail for klassegruppe. Ellers anvendes årstal i alle mails | false |
| <span id="WorkspaceSettings.NamingSettings.SecurityGroupForLevelNameStandard">WorkspaceSettings.NamingSettings.SecurityGroupForLevelNameStandard</span> | Navnestandard for gruppe for klassetrin | {INSTITUTION_NAME} {LEVEL}. klasse |
| <span id="WorkspaceSettings.NamingSettings.GlobalSecurityGroupForLevelNameStandard">WorkspaceSettings.NamingSettings.GlobalSecurityGroupForLevelNameStandard</span> | Navnestandard for global gruppe for klassetrin | {LEVEL}. klasse |
| <span id="WorkspaceSettings.NamingSettings.InstitutionDriveNameStandard">WorkspaceSettings.NamingSettings.InstitutionDriveNameStandard</span> | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”  <br><br/>Navnestandard for drevet tilknyttet institutionen | {INSTITUTION_NAME} |
| <span id="WorkspaceSettings.NamingSettings.YearlyClassGroupOnlyStudentsNameStandard">WorkspaceSettings.NamingSettings.YearlyClassGroupOnlyStudentsNameStandard</span> | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til gruppe pr klasse pr skoleår | {SCHOOL_YEAR} {INSTITUTION_NAME} {CLASS_NAME} |
| <span id="WorkspaceSettings.NamingSettings.YearlyClassGroupOnlyStudentsNameStandardNoClassYear">WorkspaceSettings.NamingSettings.YearlyClassGroupOnlyStudentsNameStandardNoClassYear</span> | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til gruppe pr klasse pr skoleår, hvis klassen ikke har startår | {SCHOOL_YEAR} {INSTITUTION_NAME} {CLASS_NAME} |
| <span id="WorkspaceSettings.NamingSettings.YearlyClassFolderNameStandard">WorkspaceSettings.NamingSettings.YearlyClassFolderNameStandard</span> | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til mappe pr klasse pr skoleår | {SCHOOL_YEAR} {CLASS_NAME} |
| <span id="WorkspaceSettings.NamingSettings.YearlyClassFolderNameStandardNoClassYear">WorkspaceSettings.NamingSettings.YearlyClassFolderNameStandardNoClassYear</span> | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til mappe pr klasse pr skoleår, hvis klassen ikke har startår | {SCHOOL_YEAR} {CLASS_NAME} |
| <span id="WorkspaceSettings.FilteringSettings.GloballyExcludedRoles">WorkspaceSettings.FilteringSettings.GloballyExcludedRoles</span> | Roller der altid ekskluderes | \[\] |
| <span id="WorkspaceSettings.FilteringSettings.ExludedRolesInInstitution">WorkspaceSettings.FilteringSettings.ExludedRolesInInstitution</span> | Roller ekskluderet pr. institution | {}  |
| <span id="WorkspaceSettings.licensingSettings.StaffLicenseProductId">WorkspaceSettings.licensingSettings.StaffLicenseProductId</span> | Produkt-ID til medarbejderlicens | ""  |
| <span id="WorkspaceSettings.licensingSettings.StaffLicenseSkuId">WorkspaceSettings.licensingSettings.StaffLicenseSkuId</span> | SKU-ID til medarbejderlicens | ""  |
| <span id="WorkspaceSettings.licensingSettings.StudentLicenseProductId">WorkspaceSettings.licensingSettings.StudentLicenseProductId</span> | Produkt-ID til elevlicens | ""  |
| <span id="WorkspaceSettings.licensingSettings.StudentLicenseSkuId">WorkspaceSettings.licensingSettings.StudentLicenseSkuId</span> | SKU-ID til elevlicens | ""  |
| <span id="WorkspaceSettings.usernameSettings.UsernameStandard">WorkspaceSettings.usernameSettings.UsernameStandard</span> | Strategi til opbygning af brugernavne for nye brugere. Se sektion omkring brugernavnestandarder. | FROM_STIL_OR_AS_UNILOGIN_RANDOM |
| <span id="WorkspaceSettings.usernameSettings.UsernamePrefix">WorkspaceSettings.usernameSettings.UsernamePrefix</span> | Præfiks til brugernavne, hvis brugernavnestandarden understøtter det | ""  |
| <span id="WorkspaceSettings.usernameSettings.RandomStandardLetterCount">WorkspaceSettings.usernameSettings.RandomStandardLetterCount</span> | Antal bogstaver brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| <span id="WorkspaceSettings.usernameSettings.RandomStandardNumberCount">WorkspaceSettings.usernameSettings.RandomStandardNumberCount</span> | Antal tal I brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| <span id="WorkspaceSettings.UserDryRun">WorkspaceSettings.UserDryRun</span> | Kør i dry run – kun log, ingen handlinger | false |
| <span id="WorkspaceSettings.RolesToBeCreatedDirectlyInGW">WorkspaceSettings.RolesToBeCreatedDirectlyInGW</span> | Roller som oprettes direkte i GW uden at have været oprettet andre steder først. | Alle roller |
| <span id="WorkspaceSettings.UseDanishCharacters">WorkspaceSettings.UseDanishCharacters</span> | Tillad danske tegn i navne | true |
| <span id="WorkspaceSettings.DeleteDisabledUsersFully">WorkspaceSettings.DeleteDisabledUsersFully</span> | Slet brugere helt efter de er suspenderet | false |
| <span id="WorkspaceSettings.DaysBeforeDeletionStudent">WorkspaceSettings.DaysBeforeDeletionStudent</span> | Dage før elev slettes efter suspendering | 60  |
| <span id="WorkspaceSettings.DaysBeforeDeletionEmployee">WorkspaceSettings.DaysBeforeDeletionEmployee</span> | Dage før ansat slettes efter suspendering | 60  |
| <span id="WorkspaceSettings.DaysBeforeDeletionExternal">WorkspaceSettings.DaysBeforeDeletionExternal</span> | Dage før ekstern slettes efter suspendering | 60  |
| <span id="WorkspaceSettings.GWTraceLog">WorkspaceSettings.GWTraceLog</span> | Aktiver detaljeret logning | false |
| <span id="WorkspaceSettings.SetContactCard">WorkspaceSettings.SetContactCard</span> | Udfyld kontaktkort for brugere | false |
| <span id="WorkspaceSettings.AddEmployeesToClassroomGroup">WorkspaceSettings.AddEmployeesToClassroomGroup</span> | Tilføj medarbejdere til classroom-gruppe. Hvis OS2skoledata skal tilføje medarbejdere, skal email’en på gruppen skrives her |     |
| <span id="WorkspaceSettings.ClassroomSettings.Enabled">WorkspaceSettings.ClassroomSettings.Enabled</span> | Aktiver Classroom-synkronisering, hvis Google Classroom administration er aktiveret i OS2skoledata Core | false |
| <span id="WorkspaceSettings.DriveType">WorkspaceSettings.DriveType</span> | Beskriver, hvordan der skal dannes drev. Enten kan der dannes et fællesdrev pr klasse (DRIVE_PR_CLASS) eller også kan der dannes et pr institution og deri en mappe pr klasse pr år (DRIVE_PR_SCHOOL_FOLDER_PR_CLASS) | DRIVE_PR_CLASS |
| <span id="WorkspaceSettings.HandlePermissionsForGroups">WorkspaceSettings.HandlePermissionsForGroups</span> | Bestemmer om OS2skoledata skal håndtere rettigheder på de grupper, den opretter | false |
