---
title: Lønkontrol opsætning
layout: default
parent: Opsætning
nav_order: 5
has_children: false
---

# Indhold

[1 Indledning](#indledning)

[2 Forudsætninger](#forudsætninger)

[3 Konfiguration](#konfiguration)

[3.1 Afviklingskadance](#afviklingskadance)

[3.2 Hvor data skal læses fra](#hvor-data-skal-læses-fra)

[3.3 Opdatering af AD](#opdatering-af-ad)

# Indledning

Dette dokument beskriver hvordan man konfigurerer Lønkontrol komponenten i OS2skoledata. Formålet med Lønkontrol komponenten er at udføre et ekstra kontroltrin op mod kommunens lønsystem, for at identificere de brugere som har en aktiv ansættelse.

Komponenten vedligeholder en lokal AD gruppe, med de brugere som har en aktiv ansættelse. Oplysningerne om den aktive ansættelse registreres også i OS2skoledata, omend OS2skoledata ikke (endnu) bruger disse oplysninger.

Integrationen kan læse lønoplysninger enten fra OPUS XML udtræk, SQL database eller direkte fra OS2sofd.

# Forudsætninger

Servicen skal afvikles under en servicekonto der har adgang til at læse fra enten OS2sofd, OPUS XML filen eller den angivne SQL database. Kun en af disse adgange er nødvendige.

# Konfiguration

Efter service er installeret, er der en konfigurationsfil ved navn appsettings.json i installationsfolderen. Denne fil har følgende sektioner som er relevante at tilpasse

## Afviklingskadance

Man angiver hvor ofte (og hvornår) servicen afvikles via et CRON udtryk i nedenstående sektion af konfigurationsfilen. Eksemplet nedenfor betyder at servicen afvikles dagligt kl 02:43 (først tal er sekunder, så minutter, så timer, derefter dato angivelser hvis det ikke skal køre dagligt)

\"JobSettings\": {

\"FullSyncCron\": \"0 43 2 \* \* ? \*\"

}

## Hvor data skal læses fra

I SyncSettings angiver man hvor data skal læses fra, og endeligt loginoplysninger til den respektive kilde

\"SyncSettings\": {

\"FetchDataFrom\": \"SOFD\",

\"OpusWagesFile\": \"c:/Temp/opus/opus_demo.xml\",

\"SQLConnectionString\": \"Server=localhost;Database=os2skoledata_checker;User Id=testbruger;Password=TestTest22;\",

\"SQLStatement\": \"SELECT employee_id, start_date, stop_date, cpr_number AS cpr FROM os2skoledata_checker.dbo.affiliations;\"

\"SOFDBaseUrl\": \"\",

\"SOFDApiKey\": \"\"

}

Feltet "FetchDataFrom" kan udfyldes med SOFD, SQL eller OPUS -- afhængig af hvad man angiver her, skal man enten udfylde de to nederste SOFD settings, de to SQL settings eller filplaceringen til OPUS filen.

## Opdatering af AD

Endeligt skal man angive relevante pegepinde til AD, så servicen kan vedligeholde medlemsskabet af en AD gruppe med alle medarbejdere med en aktiv ansættelse.

Her skal man udpege en AD gruppe (den som alle aktive ansættelser skal meldes ind i), det felt i AD hvor brugernes CPR nummer står, og endeligt en sikkerhedsgruppe til at identificere relevante brugere der skal udføres kontrol på (et filter, for at sikre at vi kun udfører kontrollen på personalet, og ikke elever eller systemkonti).

\"ActiveDirectorySettings\": {

\"ActiveEmployeesSecurityGroupDN\": \"CN=aktive_medarbejdere,OU=os2skoledata,DC=amalie,DC=dk\",

\"CprField\": \"employeeID\",

\"EmployeeSecurityGroupDN\": \"CN=alle_medarbejdere,OU=sikkerhedsgrupper,OU=os2skoledata,DC=amalie,DC=dk\"

}
