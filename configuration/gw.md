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
| JobSettings.FullSyncCron | Cron-udtryk for fuld synkronisering | 0 43 2 \* \* ? \* |
| JobSettings.DeltaSyncCron | Cron-udtryk for delta-synkronisering | 0 0/5 \* \* \* ? \* |
| JobSettings.ClassroomSyncCron | Cron-udtryk for Classroom-synkronisering, hvis det er slået til | 0 3/5 \* \* \* ? \* |
| OS2skoledataSettings.BaseUrl | Base URL til OS2skoledata API |     |
| OS2skoledataSettings.ApiKey | API-nøgle til OS2skoledata |     |
| WorkspaceSettings.ServiceAccountDataFilePath | Filsti til servicekonto JSON-fil |     |
| WorkspaceSettings.EmailAccountToImpersonate | Konto der skal impersoneres i Google |     |
| WorkspaceSettings.Domain | Domæne for Google Workspace |     |
| WorkspaceSettings.RootOrgUnitPath | Rod-OU til oprettelse af underenheder | /OS2skoledata |
| WorkspaceSettings.OUsToAlwaysCreate | Liste over OU'er der altid skal oprettes | \[\] |
| WorkspaceSettings.SuspendedUsersOU | OU til suspenderede brugere | /OS2skoledata/Suspended |
| WorkspaceSettings.DeletedOusOu | OU til “slettede” enheder | /OS2skoledata/Suspended |
| WorkspaceSettings.KeepAliveOU | OU til brugere der skal holdes aktive, hvis man anvender “forbliv aktiv”-featuren | /OS2skoledata/keepalive |
| WorkspaceSettings.HierarchyType | Strukturtype for OU-hierarki | INSTITUTION_FIRST |
| WorkspaceSettings.NamingSettings.EmployeeOUName | Navn på medarbejder-OU | Medarbejdere |
| WorkspaceSettings.NamingSettings.StudentOUName | Navn på elev-OU | Elever |
| WorkspaceSettings.NamingSettings.StudentsWithoutGroupsOUName | Navn på OU for elever uden grupper (oprettes under hver institution) | Elever udenfor grupper |
| WorkspaceSettings.NamingSettings.ClassOUNameStandard | Navnestandard for klasse-OU | {CLASS_NAME} |
| WorkspaceSettings.NamingSettings.ClassOUNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {CLASS_NAME} |
| WorkspaceSettings.NamingSettings.InstitutionOUNameStandard | Navnestandard for institution-OU | {INSTITUTION_NAME} ({INSTITUTION_NUMBER}) |
| WorkspaceSettings.NamingSettings.AllEmployeesInInstitutionDriveNameStandard | Navnestandard for drev til alle medarbejdere på en institution | {INSTITUTION_NAME} - medarbejdere |
| WorkspaceSettings.NamingSettings.ClassDriveNameStandard | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME} {CLASS_NAME} - alle |
| WorkspaceSettings.NamingSettings.ClassDriveNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME} {CLASS_NAME} - alle |
| WorkspaceSettings.NamingSettings.GlobalEmployeeDriveName | Navn på globalt medarbejderdrev | Alle medarbejdere |
| WorkspaceSettings.NamingSettings.DeletedDrivePrefix | Prefix for “slettede” drev | Slettet_ |
| WorkspaceSettings.NamingSettings.AllInInstitutionGroupNameStandard | Navnestandard for gruppe for alle i en institution | {INSTITUTION_NAME} - alle |
| WorkspaceSettings.NamingSettings.AllStudentsInInstitutionGroupNameStandard | Navnestandard for gruppe for alle elever i en institution | {INSTITUTION_NAME} - elever |
| WorkspaceSettings.NamingSettings.AllEmployeesInInstitutionGroupNameStandard | Navnestandard for gruppe for alle medarbejdere i en institution | {INSTITUTION_NAME} - medarbejdere |
| WorkspaceSettings.NamingSettings.GroupForEmployeeTypeNameStandard | Navnestandard for gruppe for medarbejdertype | {INSTITUTION_NAME} - alle - {TYPE} |
| WorkspaceSettings.NamingSettings.GroupForYearNameStandard | Navnestandard for årgangsgruppe | {INSTITUTION_NAME} - elever - {YEAR} |
| WorkspaceSettings.NamingSettings.ClassGroupNameStandard | Navnestandard for klassegruppe | {INSTITUTION_NAME}-{CLASS_NAME}-{CLASS_YEAR} - alle |
| WorkspaceSettings.NamingSettings.ClassGroupNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME}-{CLASS_NAME} - alle |
| WorkspaceSettings.NamingSettings.ClassGroupOnlyStudentsNameStandard | Navnestandard for gruppe kun for elever | {INSTITUTION_NAME}-{CLASS_NAME}-{CLASS_YEAR} - elever |
| WorkspaceSettings.NamingSettings.ClassGroupOnlyStudentsNameStandardNoClassYear | Navnestandard for ovenstående, der anvendes hvis klassen ikke har startår | {INSTITUTION_NAME}-{CLASS_NAME} - elever |
| WorkspaceSettings.NamingSettings.GlobalEmployeeGroupName | Navn på global medarbejdergruppe | Alle medarbejdere |
| WorkspaceSettings.NamingSettings.SchoolOUName | Navn på OU til skoler | Skoler |
| WorkspaceSettings.NamingSettings.DaycareOUName | Navn på OU til dagtilbud | Dagtilbud |
| WorkspaceSettings.NamingSettings.FuOUName | Navn på OU for typen FU | FU  |
| WorkspaceSettings.NamingSettings.InstitutitonStaffGroupEmailTypeName | Ord, der bruges i mail til medarbejdergruppe | staff |
| WorkspaceSettings.NamingSettings.OnlyUseYearInClassGroupEmail | Brug kun årstal i mail for klassegruppe. Ellers anvendes årstal i alle mails | false |
| WorkspaceSettings.NamingSettings.SecurityGroupForLevelNameStandard | Navnestandard for gruppe for klassetrin | {INSTITUTION_NAME} {LEVEL}. klasse |
| WorkspaceSettings.NamingSettings.GlobalSecurityGroupForLevelNameStandard | Navnestandard for global gruppe for klassetrin | {LEVEL}. klasse |
| WorkspaceSettings.NamingSettings. InstitutionDriveNameStandard | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”  <br><br/>Navnestandard for drevet tilknyttet institutionen | {INSTITUTION_NAME} |
| WorkspaceSettings.NamingSettings. YearlyClassGroupOnlyStudentsNameStandard | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til gruppe pr klasse pr skoleår | {SCHOOL_YEAR} {INSTITUTION_NAME} {CLASS_NAME} |
| WorkspaceSettings.NamingSettings. YearlyClassGroupOnlyStudentsNameStandardNoClassYear | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til gruppe pr klasse pr skoleår, hvis klassen ikke har startår | {SCHOOL_YEAR} {INSTITUTION_NAME} {CLASS_NAME} |
| WorkspaceSettings.NamingSettings. YearlyClassFolderNameStandard | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til mappe pr klasse pr skoleår | {SCHOOL_YEAR} {CLASS_NAME} |
| WorkspaceSettings.NamingSettings. YearlyClassFolderNameStandardNoClassYear | Kun relevant, hvis DriveType er ”DRIVE_PR_SCHOOL_FOLDER_PR_CLASS”<br><br>Navnestandard til mappe pr klasse pr skoleår, hvis klassen ikke har startår | {SCHOOL_YEAR} {CLASS_NAME} |
| WorkspaceSettings.FilteringSettings.GloballyExcludedRoles | Roller der altid ekskluderes | \[\] |
| WorkspaceSettings.FilteringSettings.ExludedRolesInInstitution | Roller ekskluderet pr. institution | {}  |
| WorkspaceSettings.licensingSettings.StaffLicenseProductId | Produkt-ID til medarbejderlicens | ""  |
| WorkspaceSettings.licensingSettings.StaffLicenseSkuId | SKU-ID til medarbejderlicens | ""  |
| WorkspaceSettings.licensingSettings.StudentLicenseProductId | Produkt-ID til elevlicens | ""  |
| WorkspaceSettings.licensingSettings.StudentLicenseSkuId | SKU-ID til elevlicens | ""  |
| WorkspaceSettings.usernameSettings.UsernameStandard | Strategi til opbygning af brugernavne for nye brugere. Se sektion omkring brugernavnestandarder. | FROM_STIL_OR_AS_UNILOGIN_RANDOM |
| WorkspaceSettings.usernameSettings.UsernamePrefix | Præfiks til brugernavne, hvis brugernavnestandarden understøtter det | ""  |
| WorkspaceSettings.usernameSettings.RandomStandardLetterCount | Antal bogstaver brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| WorkspaceSettings.usernameSettings.RandomStandardNumberCount | Antal tal I brugernavnestandarden FROM_STIL_OR_AS_UNILOGIN_RANDOM | 4   |
| WorkspaceSettings.UserDryRun | Kør i dry run – kun log, ingen handlinger | false |
| WorkspaceSettings.RolesToBeCreatedDirectlyInGW | Roller som oprettes direkte i GW uden at have været oprettet andre steder først. | Alle roller |
| WorkspaceSettings.UseDanishCharacters | Tillad danske tegn i navne | true |
| WorkspaceSettings.DeleteDisabledUsersFully | Slet brugere helt efter de er suspenderet | false |
| WorkspaceSettings.DaysBeforeDeletionStudent | Dage før elev slettes efter suspendering | 60  |
| WorkspaceSettings.DaysBeforeDeletionEmployee | Dage før ansat slettes efter suspendering | 60  |
| WorkspaceSettings.DaysBeforeDeletionExternal | Dage før ekstern slettes efter suspendering | 60  |
| WorkspaceSettings.GWTraceLog | Aktiver detaljeret logning | false |
| WorkspaceSettings.SetContactCard | Udfyld kontaktkort for brugere | false |
| WorkspaceSettings.AddEmployeesToClassroomGroup | Tilføj medarbejdere til classroom-gruppe. Hvis OS2skoledata skal tilføje medarbejdere, skal email’en på gruppen skrives her |     |
| WorkspaceSettings.ClassroomSettings.Enabled | Aktiver Classroom-synkronisering, hvis Google Classroom administration er aktiveret i OS2skoledata Core | false |
| WorkspaceSettings.DriveType | Beskriver, hvordan der skal dannes drev. Enten kan der dannes et fællesdrev pr klasse (DRIVE_PR_CLASS) eller også kan der dannes et pr institution og deri en mappe pr klasse pr år (DRIVE_PR_SCHOOL_FOLDER_PR_CLASS) | DRIVE_PR_CLASS |
| WorkspaceSettings.HandlePermissionsForGroups | Bestemmer om OS2skoledata skal håndtere rettigheder på de grupper, den opretter | false |
