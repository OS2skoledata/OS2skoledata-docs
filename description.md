---
title: Løsningsbeskrivelse
layout: default
nav_order: 2
has_children: false
---

# Løsningsbeskrivelse
# Indhold

[1 Indledning](#indledning)

[2 Overordnet beskrivelse](#overordnet-beskrivelse)

[2.1 Ejerskab og forankring](#ejerskab-og-forankring)

[3 Løsningsbeskrivelse](#løsningsbeskrivelse)

[3.1 Overordnet dataflow](#overordnet-dataflow)

[3.2 Konfiguration](#konfiguration)

[3.3 Integration til Active Directory](#integration-til-active-directory)

[3.3.1 Logning](#logning)

[3.4 Integration til Azure AD](#integration-til-azure-ad)

[3.5 Integration til Google Workspace](#integration-til-google-workspace)

[3.5.1 Enhedshierarkier](#enhedshierarkier)

[3.6 Integration til Apple School Manager](#apple-school-manager-integration)

[3.7 Integration til SQL Server](#integration-til-sql-server)

[3.8 Lønkontrol integration](#lønkontrol-integration)

[3.9 Brugergrænsefladen](#brugergrænsefladen)

[3.10 Årsrul](#årsrul)

[3.11 Grupper](#grupper)

[3.12 Logning](#logning-1)

[3.13 Dokumentation](#dokumentation)

[3.14 Udviklings- og leverancemodel](#udviklings--og-leverancemodel)

[3.15 Migrering fra eksisterende løsning](#migrering-fra-eksisterende-løsning)

# Indledning

Dette dokument baserer sig på den originale løsningsbeskrivelse, men er opdateret, så det afspejler den nuværende funktionalitet af OS2skoledata.

Det er en løsningsbeskrivelse af en data-integrationsløsning til skoleområdet.

Dokumentet er målrettet beslutningstagere hos de interesserede kommuner, med fokus på afklaring om anvendelse.

Bemærk at selvom løsningen skal ses som en selvstændig komponent, der ikke forudsætter eksistensen af andre specifikke produkter, er det ikke en væg-til-væg skoleløsning, der håndterer samtlige behov der findes på skole-it-området. En kommune vil stadig have behov for løsninger til inddatering af skole grunddata, en egentlig login-løsning (Identity Provider) og tilhørende komponenter.

Denne løsning håndter alene livcyklus for bruger-stamdata, som beskrevet i afsnittene nedenfor.

# Overordnet beskrivelse

Løsningen hedder OS2skoledata, og løsningen vil blive omtalt som sådan i resten af dette dokument.

OS2skoledata er grundlæggende en data-broker løsning, der har til ansvar at sikre

- At kommunens AD holdes opdateret på baggrund af data i skole-grunddata. Hermed forstået at brugerkonti oprettes, nedlægges, flyttes og at stamdata og gruppemedlemsskaber på disse holdes ajour. Derudover vedligeholdes et enhedshierarki baseret på institutionerne og grupperne fra STIL.

- At kommunens skole-grunddata stilles til rådighed for kommunen i et SQL-replika, som etableres on-premise i kommunens eget SQL cluster. Til databasen anvendes der MariaDB.

- At kommunens Google Worksspace data holdes ajour, på samme måde som kommunens AD, hermed forstået at brugere oprettes, nedlægges og holdes ajour, herunder at stamdata og rettigheder til fællesdrev ajourføres.

- At kommunens Azure AD holdes ajour, hermed forstået oprettelse og nedlæggelse af brugere, samt vedligehold af sikkerhedsgrupper, fx til Teams m.m. der afspejler klasse-tilhørsforhold. I Azure AD vedligeholdes der ikke et enhedshierarki.

- At der via en separat on-premise service kan vedligeholdes en sikkerhedsgruppe med aktive ansættelser via opslag i en OPUS-fil, en SQL database eller OS2sofd

For at understøtte forskelligheden på tværs af kommunerne, etableres de fornødne konfigurationsmuligheder i disse integrationer, så navnestandarder, OU strukturer m.m. kan tilpasses kommunens behov.

Endeligt etableres en brugergrænseflade til styring af data-flowet, så kommunen selv kan pause, inspicere og starte dataflowet, med det formål at have bedre kontrol over større ændringer, fx ved årsrul og lignende hændelser.

## Ejerskab og forankring

OS2skoledata, som navnet antyder, udvikles som et Open Source produkt, med ejerskabet foranket i OS2 samarbejdet, hermed forstået at ejerskabet ligger hos medlemskommunerne i OS2.

Det etableres dermed også en styregruppe og koordinationsgruppe i OS2-regi, der kan drive udviklingen af OS2skoledata videre, efter lanceringen af den første version.

# Løsningsbeskrivelse

I dette afsnit gennemgåes de enkelte del-komponenter i OS2skoledata løsningen.

## Overordnet dataflow

Udlæsning af data fra skole-grunddata sker via snitfladen WS-17 (fuld myndighed). Det er muligt at lave op til 4 udlæsninger per dag for en given institution, og OS2skoledata sættes op til at foretage disse udlæsninger på optimale tidspunkter, for at sikre et effektivt flow af hændelser indenfor samme arbejdsdag.

Data trækkes fra WS-17 ind i OS2skoledata Core, der er en central komponent driftet af Digital Identity. Alternativt kan kommunen vælge selv at indlæse data i OS2skoledata via Import API'et. Det er muligt at indlæse ansatte og eksterne via API'et. Hvis man vælger at administrere data via API'et, vil det være dette, der er styrende for oprettelser og sletninger uanset hvad der sker i STIL. Data fra lokal kilde vil dog blive beriget med data fra STIL. Det er muligt at konfigurere hvilke felter, der må vedligeholdes af STIL. Hvor der indlæses data fra (STIL eller API og STIL) og hvilke felter STIL må berige, styres via konfigurationen i OS2skoledata Core. Det er muligt at oprette "ApiOnly" elever via import-API'et. Disse elever opdateres ikke af STIL, da de ikke eksisterer deri, og de skal placeres på en "kunstig" institution, som kan oprettes via brugergrænsefladen (hvis modulet er slået til).

På baggrund af ændringer i data, dannes de respektive dataændringer som hændelsesbeskeder, der lægges i en udgående kø.

Den udgående kø indeholder en liste med objekter, der skal oprettes, opdateres eller slettes.

De enkelte hændelser aftages af såkaldte klienter. Klienterne kører delta sync på konfigurable tidspunkter hvor den læser fra denne kø. Derudover vil klienterne på et konfigurabelt tidspunkt køre fuld sync, hvor den læser alt ud fra databasen og vedligeholder ud fra det. De fleste af disse klienter driftes også af Digital Identity, og indgår i det samlede driftsetup for OS2skoledata. Klienten der står for opdatering af data i skolens on-premise AD, afvikles dog lokalt hos kommunen som en Windows Service.

I brugergrænsefladen er køen synlig, så man kan se kommende hændelser, der ligger og venter på at blive behandlet af klienterne. På siden, hvor de kommende hændelser vises, vælges hvilken klient man vil se kommende ændringer for. Det er muligt, fra brugergrænsefladen, at stoppe afviklingen pr klient -- en slags "pause-funktion". Mens pause-funktionen er slået til, hober hændelser sig op ind "core" komponenten, og afventer at pause-markeringen fjernes.

Funktionens primære formål er at kunne udføre kvalitetssikring af dataflowet under implementeringen, så man kan se effekten af indlæste data, uden reelt at udføre den, og i praksis kunne korrigere i kildedata inden klienterne igen sættes i gang.

## Konfiguration

For at understøtte den forskellighed der findes i kommunerne, skal det være muligt at konfigurere en række ting. Der er en konfigurationsfil til core og hver klient. De klienter, der ikke er on-premise, kan kun konfigureres af Digital Identity. I on-premise klienterne er der en konfigurationsfil, der kan tilgås af kommunen selv. Den skal tilpasses af kommunen eventuelt med hjælp fra Digital Identity.

Mange elementer i løsningen er konfigurable og der kan læses om konfigurationsmulighederne i dokumentet omkring konfiguration.

## Integration til Active Directory

Integrationen til Active Directory udvikles som en Windows Service, der installeres lokalt i kommunens infrastruktur. Denne service kommunikerer ud til OS2skoledata, så der er ikke behov for nogen speciel netværksåbninger (ud over udgående trafik på port 443 til OS2skoledata, hvilket normalt er åbent som standard).

Integrationen er ansvarlig for at sikre følgende

- AD brugerkonti oprettes og nedlægges (se nedenfor) på baggrund af hændelser fra OS2skoledata core komponenten. Der oprettes brugerkonti jf den brugernavnestandard som er opsat i konfigurationen, men eksisterende brugerkonti der ikke følger navnestandarden vil fortsætte med deres eksisterende brugernavn. Bemærk at kodeord ikke styres via OS2skoledata.

  - Filtrering -- det er muligt at undtage specifikke roller fra at få en AD konto. Fx "Role = Barn" hvis man ikke ønsker at børn i dagtilbud skal have en AD konto. Denne filtrering kan opsættes globalt (det globale filter gælder på tværs af alle institutioner), samt suppleres med et filter for enkelte institutioner (fx hvis en given institution ikke ønsker at Eksterne skal have en AD konto).

- Mapning af attributter til AD konti.

  - Et sæt af attributter fra databasen kan overføres til AD kontoens attributter. De felter, der udfyldes som standard er:

    - Name: {fornavn} {efternavn} ({brugernavn})

    - GivenName: {fornavn}

    - Surname: {efternavn}

    - SamAccountName: {brugernavn}

    - DisplayName: {fornavn} {efternavn}

    - UserPrincipalName: {brugernavn}{emaildomæne}

    - Password: random bogstaver og tal på 36 tegn (skal skiftes ved login)

  - Der kan vedligeholdes flere felter, disse konfigureres i konfigurationsfilen og der kan læses om dem i dokumentet omhandlende konfigurationen.

- Nedlæggelse af brugere sker blot ved disabling af AD kontoen. Når en AD konto er disabled, bliver den flyttet over i en OU angivet i konfigurationen, og der oprettes en under-OU med dato-stempel, hvor AD kontoen placeres. Kommunen kan selv vælge hvornår og hvor ofte de vil udføre fysisk sletning, og kan anvende dato-stemplerne til at se hvor gammel AD kontoen er. Ved reaktivering af en eksisterende AD konto flyttes den ud fra OU strukturen og over i den institution den hører til. Der er mulighed for opsætning af automatisk sletning et konfigurabelt antal dage efter kontoen er disabled. Antallet af dage kan differentieres baseret på om brugeren er en elev, en medarbejder eller en ekstern.

- Vedligehold af en OU struktur der afspejler institutionernes organisation (bemærk navne OU'erne følger den opsatte konfiguration). I praksis er det

  - En rod OU hvor alt oprettes under (konfigurabelt)

  - En OU til institutionstypen (fx Skoler og Dagtilbud) under rod OU'en

  - En OU per institution under den relevante type OU

  - Underindeling af hver institutions-OU i "elever", "personale", "sikkerhedsgrupper" og evt ekstra faste OU'ere der altid laves jf konfigurationen (det kan fx være "servicekonti", "eksterne" eller hvad man nu ønsker der skal oprettes fast -- bemærk at OS2skoledata ikke selv putter brugere/data ind i disse ekstra OU'ere, så de er til lokalt brug i kommunen)

  - OU'en for elever underindeles i klassetrin (fx "1a", "7b", osv)

- Der udføres ikke sletninger på OU strukturene. OU'er, der ikke længere er i STIL, flyttes i stedet til en OU angivet i konfigurationen, og der oprettes en under-OU med dato-stempel, hvor den "slettede" OU placeres. Kommunen kan selv vælge hvornår og hvor ofte de vil udføre fysisk sletning af OU'erne under OU'en der er konfigureret til placering af "slettede" OU'er.

- AD brugerkonti placeres i den OU hvor de hører til organisatorisk -- for brugere, som er tilknyttet flere institutioner, vælges én tilfældig af tilknytningernes OU hvor de indplaceres. Man kan lokalt vælge at flytte dem rundt, og så længe AD kontoen er indplaceret i en OU som de er tilknyttet jf OS2skoledata, vil OS2skoledata ikke flytte dem. Hvis en AD konto flyttes væk fra en OU som de bør være i jf OS2skoledata, så flyttes de tilbage ved næste opdatering.

- Oprettelse af, og indplacering i, sikkerhedsgrupper der afspejler klasser, institutioner og roller. Sikkerhedsgrupperne placeres i OU'en "sikkerhedsgrupper" under den institution som gruppen hører til. Bemærk her at en bruger godt kan høre til sikkerhedsgrupper fra forskellige institutioner, selvom deres bruerkonto er indplaceret i OU'en for én specifik institution.

- Mulighed for kørsel af powershell ved oprettelse/reaktivering af en bruger samt ved deaktivering af en bruger. Kommunen laver selv powershell scripts udfra deres egne behov. Når powershell scriptet køres, sendes brugernavn, navn og rolle med. Hvis man har behov for mere info på brugeren, kan det konfigureres, så hele brugerobjektet, sendes til powershell scriptet som JSON.


### Logning

Opdateringen af AD sker on-premise via en lokal klient (windows service). Den lokale klient logger alle udførte handlinger i AD'et til en logfil. Kommunen kan selv konfigurere rotationsregler og retention policies for logfilen i konfigurationsfilen for den lokale klient.

## Integration til Azure AD

Nogle kommuner anvender Azure AD alene til styring af adgange (til Teams rum), mens andre opretter deres brugere direkte i Azure AD (fx elever som ikke skal oprettes i on-premise AD i nogle kommuner).

Til formålet er der en klient, som kan udføre begge opgaver, baseret på den opsatte konfiguration. Denne klient sikrer dermed

- Oprettelse og nedlæggelse af brugere

  - Vedligehold af et sæt af attributter

    - givenName: {fornavn}

    - surname: {efternavn}

    - displayName: {fornavn} {efternavn}

    - mailNickname: {brugernavn}

    - userPrincipalName: {brugernavn}{domæne}

    - mail: {brugernavn}{domæne}

    - companyName: OS2skoledata (OS2skoledatas mærke, for at vide hvilke brugere den administrerer)

    - employeeId: {cpr} (hvis man ønsker at have cpr i Azure)

    - department/employeeId: {UNIID} (konfigureres hvilken man vil anvende)

    - Password: random bogstaver og tal på 36 tegn (skal skiftes ved login)

  - Derudover vedligeholdes et skema, som OS2skoledata selv opretter for at kunne gemme flere informationer på brugerne. Skemaet hedder OS2skoledata.

    - globalRole: STUDENT/EMPLOYEE/EXTERNAL

    - disabledDate: datoen, hvor brugeren er blevet disabled

- Oprettelse og nedlæggelse af sikkerhedsgrupper og styring af medlemmer af disse

- Oprettelse og nedlæggelse af teams for klasser og for medarbejdere på en institution

- Der er mulighed for opsætning af automatisk sletning et konfigurabelt antal dage efter kontoen er disabled. Antallet af dage kan differentieres baseret på om brugeren er en elev, en medarbejder eller en ekstern.

## Integration til Google Workspace

Nogle kommuner anvender Google Workspace, og der etableres derfor en klient til oprettelse, nedlæggelse og opdatering af brugere heri. Derudover vedligeholdes et enhedshierarki og en række grupper og drev.

Integrationen sikrer dermed

- Oprettelse og nedlæggelse af brugere i Google Workspace.

  - Vedligehold af et sæt af attributter

    - PrimaryEmail: {brugernavn}{domæne}

    - GivenName: {fornavn}

    - FamilyName: {efternavn}

    - FullName: {fornavn} {efternavn}

    - OrgUnitPath: Sti til OU'en hvor brugeren skal placers

    - Password: random bogstaver og tal på 36 tegn

  - Mulighed for vedligehold af kontaktkort

    - Der oprettes en organisation, der knyttes til brugeren pr tilknyttet institution. Det er disse organisationer, der bestemmer hvad der vises på kontaktkortet

  - Derudover vedligeholdes et skema, som OS2skoledata selv opretter for at kunne gemme flere informationer på brugerne. Skemaet hedder OS2skoledata.

    - ROLE: STUDENT/EMPLOYEE/EXTERNAL

    - DELETED_DATE: datoen, hvor brugeren er blevet suspenderet

- Oprettelse og vedligehold af OU struktur in Google Workspace. Her er der mulighed for at vælge hvilken der passer bedst til kommunen. Se de mulige under punkt 3.5.1 Enhedshierarkier.

- Mulighed for at oprette og vedligeholde drev efter to forskellige modeller. Enten kan der oprettes et fællesdrev til medarbejder inden for en institution og et fællesdrev pr klasse, der følger klassen gennem helle skolegangen. Ellers kan der oprettes et fællesdrev pr institution, hvor kommunen selv styrer adgange, derudover oprettes der en mappe pr klasse pr skoleår, der deles med relevante medarbejdere og elever.

- Tildeling af faste licenser baseret på elev/voksen indelingen. Og licenser skal fjernes når en brugerkonto deaktiveres, og tildeles igen når brugerkontoen aktiveres.

- Oprettelse og nedlæggelse af grupper og styring af medlemmer af disse

- Der er mulighed for opsætning af automatisk sletning af brugere et konfigurabelt antal dage efter kontoen er suspenderet. Antallet af dage kan differentieres baseret på om brugeren er en elev, en medarbejder eller en ekstern.

### Enhedshierarkier

#### Institutioner først:

Herunder vises et eksempel på standardenhedsstrukturen. Det er også den, der tilbydes i AD og Azure AD integrationen.

- OS2skoledata

  - Kommuneinstitution (der kan være flere, der alle vil blive opettet under \"OS2skoledata\")

    - Medarbejdere

    - Elever (vil nok være tom)

  - FU

    - Institution

      - Medarbejdere

      - Elever

        - klasse

  - Dagtilbud

    - Institution

      - Medarbejdere

      - Elever

        - klasse

  - Skoler

    - Institution

      - Medarbejdere

      - Elever

        - klasse

#### Institutioner sidst:

- OS2skoledata

  - Elever

    - Institution

      - klasse

  - Medarbejdere

    - institution

## Apple School Manager integration

Dette er en selvstændig komponent. Integrationen til Apple School Manager hiver via et API kald alt aktuel data ud fra OS2skoledata core. I integrationen dannes seks csv filer efter Apple standard - students.csv, staff.csv, locations.csv, courses.csv, classes.csv og roster.csv. Filerne uploades til Apple via SFTP.

## Integration til SQL Server

Dette er en selvstændig windows service. Den skriver til en SQL database, hvor den vedligeholder en struktur der datamodel-mæssigt minder om strukturen i WS-17, så man har et lokalt replika af OS2skoledata databasen liggende til lokalt brug.

Bemærk at en 100% identisk datamodel med den SQL struktur som man evt måtte have i dag, ikke er mulig. Data vil afspejle strukturen i WS-17, så data vil formodentligt være meget tæt på identiske med de data man i dag har i sin SQL database, men af praktiske årsager kan der ikke leveres et 100% identisk SQL replika af det man får fra anden leverandør.

Løsningen baserer sig på en MariaDB SQL databaseteknologi. Denne er valgt da den er licensfri, og ikke alle kommuner har MS SQL serverlicenser på skoleområdet.

## Lønkontrol integration

Dette er en selvstændig windows service. Denne service vedligeholder en sikkerhedsgruppe kun med aktive ansættelser. Det konfigureres om servicen skal tjekke aktive ansættelser i SOFD, en database eller en OPUS fil. For at en bruger tilføjes til sikkerhedsgruppen med aktive ansættelser, skal brugeren være i OS2skoledata og have en aktiv ansættelse.

Udover at vedligeholde sikkerhedsgruppen, sendes ansættelserne til OS2skoledat, hvor de gemmes i databasen. De bruges ikke til noget i dag, men så er de der, hvis der skal laves noget med dem i fremtiden.

## Brugergrænsefladen

Der er en brugergrænseflade, hvor adgangen styres via SAML (AD FS eller hvad man nu kører lokalt som IdP).

I brugergrænsefladen kan man

- Se afventende hændelser pr klient

- Se og administrere klienter. Derudover kan man pause klienter, hvis man ønsker at de ikke skal opdateres i en periode. Der findes tre forskellige typer af klienter. Man vælger typen, når man opretter klienten. Som standard er typen "Adgang til API'erne bortset fra import API'et". Den type vil være tilstrækkelig for de fleste formål. Hvis der er brug for at der sættes kodeord for indskolingselever (konfigurabel feature) vælges typen "Adgang til API'erne inklusiv kodeord på brugere bortset fra import API'et". Hvis der skal opsættes en klient til indlæsning af data via import API'et vælges typen "Adgang udelukkende til import API'et".

- Se indlæste institutioner og låse dem op ved årsrul. Derudover kan man få en mail ved årsrul eller hvis antallet af brugere i en institution i STIL afviger meget fra det antal der er i databasen. Hvis antallet af personer afviger meget, kan man tilgå en side i pr insititution, hvor man kan se ændringen og godkende den.

- Se liste over alle institutionsnumre som der pt indlæses data for

- Konfigurable moduler

  - Kodeordsadministration for elever. Opsæt hvem, der må skifte kodeord på elever. Log ind som skolemedarbejder eller forældre og skift kodeord på tilknyttede elever. Derudover har skolemedarbejdere mulighed for at få printet klasselister for tilknyttede klasser. Der er mulighed for at konfigurere at man ikke ønsker at administrere kodeord i OS2skoledata, men bare gerne vil kunne tilgå klasselisterne.

  - Forbliv aktiv. Mulighed for at opsætte brugernavne, der skal holdes aktive selvom de ikke længere er i STIL eller er markeret som slettet via import API'et.

  - Google Classrooms. Der kan opsættes Google Classroom administratorer. Disse kan så tilgå en sidde, hvor det er muligt at bestille overdragelse eller arkivering af et classroom. Google Workspace integrationen læser så fra denne kø og udfører de bestilte handlinger fx hver 5. minut.

  - Teamsadministratorer. Hvis OS2skoledata skal stå for oprettelse af teams til medarbejdere på institutionerne, skal der opsættes hvem der skal være ejer på medarbejderteamet på institutionen.

  - Kunstige institutioner. Hvis denne er slået til, er der mulighed for at oprette kunstige institutioner via brugergrænsefladen. Det vil sige institutioner, der ikke eksisterer i STIL og derfor ikke indgår i STIl sync'en. Disse kunstige institutioner kan fx bruges til at placere apiOnly brugere fra import-API'et på.

## Årsrul

Ved årsrul beholdes enheder, grupper, drev og teams så vidt muligt. Der laves et decideret rul, så hvis OS2skoledata kan matche den gamle klasse med en ny klasse, vil navnet bare blive ændret - fx 2A i 23/24 til 3A i 24/25.\
Det tjekkes først om en hel årgang i det gamle skoleår kan matches til en hel årgang i det nye skoleår -- fx 2A, 2B, 2C i 23/24 til 3A, 3B, 3C i 24/25. Hvis det kan lade sig gøre, vil der ikke blive oprettet nye grupper, de eksisterende vil bare blive omdøbt.\
Hvis der ikke kan laves match på en hel årgang, kigges der på hver enkel klasse på årgangen. Her kigges der på om eleverne i klasserne matcher. Hvis en klasse i det nye år har 70% af de samme elever i det gamle skoleår, omdøbes den gamle klasse til det nye klassenavn.\
Til sidst, hvis der ikke kan matches på en af disse to måder, bliver klassen oprettet på ny.

I 0., 10. klasse og øvrige (fx "DT" eller "Andet") bliver der ikke forsøgt at lave et match, og der oprettes altid nye klasser.

Det er muligt at OS2skoledata automatisk kan sende en mail, når der sker årsrul. I brugergrænsefladen under "institutioner", kan der konfigureres en eller flere kontakemails. Det er også denne side i brugergrænsefladen man skal tilgå for at låse institutionerne op igen efter årsrul.

## Grupper

OS2skoledata har mulighed for at vedligeholde et stort sæt af grupper. Herunder listes de alle, og det er valgfrit hvilke der oprettes. Det kan også ses af tabellen hvilke integrationer, der understøtter gruppen.

| **Gruppe**                                                                                          | AD  | AAD | GW  |
|------------------------------------------------------------------------------------------------------|-----|-----|-----|
| Global gruppe til elever                                                                             | ✓   | ✓   |     |
| Global gruppe til medarbejdere                                                                       | ✓   | ✓   | ✓   |
| Global gruppe pr årgang, hvor medlemmer ændrer sig, men navnet gør ikke fx 1. klasse                 | ✓   | ✓   | ✓   |
| Global gruppe pr type medarbejder pr type institution                                                | ✓   |     |      |
| Gruppe til alle i en institution                                                                     |✓    | ✓   | ✓   |
| Gruppe til alle elever i en institution                                                              |✓    | ✓   | ✓   |
| Gruppe til alle medarbejdere i en institution                                                        |✓    | ✓   | ✓   |
| Gruppe til alle i en klasse                                                                          |✓    | ✓   | ✓   |
| Gruppe til alle elever i en klasse                                                                   |✓    |     | ✓   |
| Gruppe til alle medarbejdere knyttet til en klasse                                                   |✓    |     |     |
| Gruppe pr type medarbejder i institutionen                                                           |✓     |    | ✓   |
| Gruppe pr årgang med året hvor de er startet i 0. klasse fx elever 2024                              |✓     |    | ✓   |
| Gruppe pr årgang, hvor medlemmer ændrer sig, men navnet gør ikke fx 1. klasse                        |✓     | ✓   | ✓   |
| Gruppe til andre gruppetyper end hovedgrupper. Typer: årgang, retning, hold, team, andet             |✓     |      |     |


## Logning

Hver klient logger alle de handlinger, de udfører. I on-premise integrationerne vil logfilen blive gemt on-premise og som standard gemmes logs for de seneste ti dage. I de øvrige integrationer gemmes loggen i skyen, og kan tilgåes af Digital Identity.

I AD integrationen er der lavet en loguploader feature, der gør at Digital Identity kan anmode om loggen og automatisk få den tilsendt, da den jo kun kan tilgås på serveren af kommunen normalt.

## Dokumentation

Der er dokumentation af løsningen, som dækker

- En opdateret løsningsbeskrivelse, der afspejler det leverede

- Installations- og konfigurationsvejledninger til alle on-premise klienter

- Implementeringsvejledning til indgåelse af aftaler til WS-17 og evt andre integrationer/aftaler/servicekonti til Azure og Google Workspace

- Detaljeret beskrivelse af konfigurationsmuligheder

- Arkitekturbeskrivelse

- Beskrivelse af navnestandarder

## Udviklings- og leverancemodel

OS2 skoledata er et OS2-produkt. Udviklingsønsker oprettes i Jira og behandles af koordinationsgruppen, der vælger om opgaven afvises eller bestilles. Kommuner har også mulighed for selv at betale for videreudvikling.

De enkelte kommuner kan indgå driftsaftaler med Digital Identity på løsningen.

## Migrering fra eksisterende løsning

Da alle kommunerne i dag har en eller anden form for løsningen til ovenstående, vil der være en migreringsopgave. Denne aftales med kommunen i forbindelse med indgåelse af driftsaftalen, men vil i praksis indeholde en plan for overgangen fra den eksisterende løsning til OS2skoledata.

Det primære fokus vil være at sikre at eksisterende data vil kunne fortsætte med at virke efter overgangen til OS2skoledata, så eksisterende brugere ikke påvirkes.

Det anbefales på det kraftigste at der opbygges en ny OU struktur, og de eksisterende brugere flyttes over i denne struktur. Det samme kunne gøre sig gældende for grupper (man kan så bruge noget gruppe-i-gruppe styring til at lave en blød overgang på gruppestyringen). Brugerne flyttes automatisk af OS2skoledata og flytningen er derfor ikke en manuel opgave. Detaljerne for dette aftales med den enkelte kommune.
