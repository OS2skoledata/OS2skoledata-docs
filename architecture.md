---
title: Arkitektur
layout: default
nav_order: 3
has_children: false
---

# Indhold

[1 Overordnet dataflow](#overordnet-dataflow)

[2 Kode](#kode)

[2.1 Overordnet](#overordnet)

[2.2 OS2skoledata core](#os2skoledata-core)

[2.3 Active Directory integration (on-premise)](#active-directory-integration-on-premise)

[2.4 Google Workspace integration](#google-workspace-integration)

[2.5 Azure AD integration](#azure-ad-integration)

[2.6 SQL sync (on-premise)](#sql-sync-on-premise)

[2.7 Lønkontrol (on-premise)](#lønkontrol-on-premise)

[3 Jobs](#jobs)

# Overordnet dataflow

Dataflow-arkitekturen er illusteret nedenfor

![Diagram describing the architecture](/assets/flow_udvidet.png)

OS2skoledata fungerer som det centrale bindeled mellem nationale skoledata, lokale infrastrukturer og cloud-baserede tjenester. Systemet modtager som standard data fra Skolegrunddata via STIL's WS17-webservice. Disse data omfatter oplysninger om skoler, elever, klasser og ansatte, som behandles i OS2skoledata core og gemmes i en database, der svarer nogenlunde til datastrukturen i STIL. På baggrund af disse oplysninger oprettes, opdateres og nedlægges brugere, grupper og enheder automatisk i en række integrerede systemer. I stedet for at anvende WS17 til at styre data, kan kommunen importere data for ansatte og eksterne ind i OS2skoledata via import-API’et. Hvis denne metode vælges vil det lokale data være styrende for alle oprettelser og sletninger, uanset hvad der sker i STIL. Det vil dog være muligt at berige en række felter med data fra STIL. Det er muligt at oprette "ApiOnly" elever via import-API'et. Disse elever opdateres ikke af STIL, da de ikke eksisterer deri, og de skal placeres på en "kunstig" institution, som kan oprettes via brugergrænsefladen (hvis modulet er slået til). 

På lokalt niveau integrerer OS2skoledata med Active Directory (AD), hvor det kan styre brugere, grupper og enheder. Samtidig er der mulighed for at opretholde en lokal database gennem SQLSync (baseret på MySQL eller MariaDB), der spejler de relevante data fra OS2skoledata core til brug i f.eks. statistik og lokale integrationer. Derudover er der en integration, der vedligeholder en sikkerhedsgruppe med aktive ansættelser. Dette gøres via løndata (OPUS, SQL eller OS2sofd) for at validere og sikre, at kun personer med aktive ansættelser oprettes og tilknytning i STIL (via OS2skoledata) er medlemmer af sikkerhedsgruppen. Disse løndata bruges også til at opdatere OS2skoledata med information om aktuelle ansættelser.

På cloud-siden integreres OS2skoledata med både Google Workspace og Azure AD, som hver især understøtter forskellige aspekter af skolernes digitale infrastruktur.

I integrationen med Google Workspace sørger OS2skoledata for automatisk oprettelse, opdatering og nedlæggelse af brugere, enheder, drev og grupper. Dette sikrer, at skolernes Google-miljø altid afspejler de aktuelle oplysninger om elever og ansatte fra STIL.

Med Azure AD håndterer OS2skoledata tilsvarende oprettelse, opdatering og nedlæggelse af brugere, grupper og teams. Integration med Azure AD gør det muligt at understøtte Microsoft 365-miljøer og Microsoft Teams som samarbejdsplatform, hvor f.eks. klasser automatisk kan oprettes som teams med de rette deltagere og rettigheder. Dette bidrager til at automatisere og forenkle den digitale administration på skolerne.

Integrationen til Apple School Manager hiver via et API kald alt aktuel data ud fra OS2skoledata core. I integrationen dannes seks csv filer efter Apple standard - students.csv, staff.csv, locations.csv, courses.csv, classes.csv og roster.csv. Filerne uploades til Apple via SFTP.

Alt dette styres centralt fra OS2skoledata core, hvorfra al databehandling og systemintegration koordineres.

Derudover tilbydes en webbaseret brugergrænseflade, hvor administratorer kan få overblik over kommende ændringer, administrere klienter og låse institutioner op i forbindelse med årsrul. Der er mulighed for at medarbejdere og forældre kan logge ind og håndtere tilknyttede elevers kodeord.

Det samlede setup sikrer en høj grad af automatisering og konsistens på tværs af systemlandskabet i en kommune.

# Kode

## Overordnet

Alt kode vedrørende OS2skoledata ligger i en mappe. I mappen ligger en mappe til hver del af OS2skoledata. Der er en mappe til dokumentationen, til OS2skoledata core, til AD integratione, til Google Workspace integrationen, til Azure AD integrationen, til SQL sync og til affiliation checker.

Nedenstående information omkring kørsel af integrationerne, er kun relevant hvis kommunen selv drifter løsningen. Hvis Kommunen kører løsningen gennem en driftsleverandør, fx Digital Identity, vil denne stå for alt omkring drift og udlevering af installers.

## OS2skoledata core

OS2skoledata core er lavet med Java 17 og Spring boot 2.7.4.  
Projektet er afhængig af en MariaDB database for at køre. Der skal oprettes et skema til OS2skoledata, og der skal sørges for at der er en brugerkonto, der har adgang til dette skema.

I projektets kode findes dk.digitalidentity.os2skoledata.config.OS2SkoleDataConfiguration hvor OS2skoledata indstillingerne findes. De har defaultværdier, som overskrives af application.properties. Der kan læses mere om konfigurationsmulighederne i dokumentet omkring konfiguration. Udover de indstillinger der findes i klassen beskrevet ovenfor, er der nogle indstillinger der er generelle for denne type projekt fx portnummer. I default.properties findes en række standardværdier, man ikke behøver ændre, der er dog mulighed for at ændre dem, hvis man har behov for det.

Inden man kører projektet er der en række indstillinger der skal sættes i application.properties:

| Indstilling | Beskrivelse |
| --- | --- |
| spring.datasource.url | Skal pege på det oprettede OS2skoledata skema. Det kunne fx se sådan her ud jdbc:mysql://localhost/os2skoledata?useSSL=false&serverTimezone=UTC |
| spring.datasource.username | sættes til brugernavnet på den bruger, der er oprettet til at tilgå databasen |
| spring.datasource.password | sættes til kodeordet på den bruger, der er oprettet til at tilgå databasen |
| os2skoledata.stilUsername | Brugernavnet der anvendes til at tilgå STIL |
| os2skoledata.stilPassword | Kodeordet der anvendes til at tilgå STIL |
| os2skoledata.institutions\[0\].institutionNumber | En række pr institution, der ska hentes fra STIL. Tallet (her 0) stiger pr institution. Navnet på institutionen |
| os2skoledata.institutions\[0\].type | En række pr institution, der ska hentes fra STIL. Tallet (her 0) stiger pr institution. Typen på institutionen. Kan være SCHOOL, DAYCARE, MUNICIPALITY |

Når disse indstillinger er sat, kan projektet køres fra en terminal åbnet i os2skoledata/core. Her skriver man ”mvn clean install spring-boot:run” hvorefter projektet køres.

## Active Directory integration (on-premise)

Active Directory integrationen er lavet i c# dotnet 6.  
Projektet er ikke afhængigt af en database, men henter data fra OS2skoledata, så en kørende OS2skoledata Core er krævet.

I appsetting.json, skal der tilpasses nogle indstillinger for at det kommer til at virke:

| Indstilling | Beskrivelse |
| --- | --- |
| OS2skoledataSettings.BaseUrl | Url til den kørende OS2skoledata Core |
| OS2skoledataSettings.ApiKey | API-nøgle til den kørende OS2skoledata Core |
| ActiveDirectorySettings.RootOU | DistinguishedName på den enhed i AD, som OS2skoledata skal bygge hierarkiet under |
| ActiveDirectorySettings.DisabledUsersOU | DistinguishedName på den enhed i AD, som OS2skoledata skal flytte disablede brugere over i |
| ActiveDirectorySettings.RootDeletedOusOu | DistinguishedName på den enhed i AD, som OS2skoledata skal flytte enheder, der ikke længere er i STIL over i |

Projektet kan køres fra Visual Studio eller der kan bygges en installer. I Visual Studio bygges en installer ved at trykke på ”Build”, så ”Publish Selection”. På den side oprettes der er en ny profil ved at trykke på ”New profile” der åbnes en popup. I denne vælges ”Folder”. Den foreslår automatisk en mappe, men der kan vælges en anden, hvis projektet bygges et andet sted. Der trykkes ”Finish”. Når den nye profile er oprettet, trykker man på ”Publish”. Nu er man klar til at bygge selve installeren. Man går i stifinderen og under os2skoledata\\os2skoledata-ad-sync\\Installer. Her ligger en setup.iss fil, den compiles via Inno Setup, og der dannes en exe fil.

## Google Workspace integration

Google Workspace integrationen er lavet i c# dotnet 6.  
Projektet er ikke afhængigt af en database, men henter data fra OS2skoledata, så en kørende OS2skoledata Core er krævet.

I appsetting.json, skal der tilpasses nogle indstillinger for at det kommer til at virke:

| Indstilling | Beskrivelse |
| --- | --- |
| OS2skoledataSettings.BaseUrl | Url til den kørende OS2skoledata Core |
| OS2skoledataSettings.ApiKey | API-nøgle til den kørende OS2skoledata Core |
| WorkspaceSettings.ServiceAccountDataFilePath | Sti til den fil, der giver adgang til Google Workspace |
| WorkspaceSettings.EmailAccountToImpersonate | Email på den bruger i Google Workspace, der skal impersoneres |
| WorkspaceSettings.Domain | Google Workspace domæne |
| WorkspaceSettings.RootOrgUnitPath | Sti til den enhed i Google Workspace, som OS2skoledata skal bygge hierarkiet under |
| WorkspaceSettings.SuspendedUsersOU | Sti til den enhed hvor OS2skoledata skal flytte suspenderede brugere over i |
| WorkspaceSettings.DeletedOusOu | Sti til den enhed hvor OS2skoledata skal flytte enheder der ikke længere er i STIL over i |

Projektet kan bygges fra Visual Studio ved at trykke ”Build” 🡪 ”Build Solution”. Projektet kan køres fra Visual Studio ved at trykke på den grønne pil (start) i topbaren.

## Azure AD integration

Azure AD integrationen er lavet med Java 17 og Spring boot 3.0.1.

Projektet er ikke afhængigt af en database, men henter data fra OS2skoledata, så en kørende OS2skoledata Core er krævet.

I application.properties, skal der tilpasses nogle indstillinger for at det kommer til at virke:

| Indstilling | Beskrivelse |
| --- | --- |
| skole.os2skoledata.baseUrl | Url til den kørende OS2skoledata Core |
| skole.os2skoledata.apiKey | API-nøgle til den kørende OS2skoledata Core |
| skole.azureAd.clientID | ClientId til adgang i Azure |
| skole.azureAd.clientSecret | ClientSecret til adgang i Azure |
| skole.azureAd.tenantID | TenantId til adgang i Azure |

Projektet køres fra en terminal åbnet i os2skoledata/os2skoledata-azure-ad-sync. Her skriver man ”mvn clean install spring-boot:run” hvorefter projektet køres

## Apple School Manager integration

Apple School Manager integrationen er lavet i c# dotnet 6.  
Projektet er ikke afhængigt af en database, men henter data fra OS2skoledata, så en kørende OS2skoledata Core er krævet.

I appsetting.json, skal der tilpasses nogle indstillinger for at det kommer til at virke:

| Indstilling | Beskrivelse |
| --- | --- |
| OS2skoledataSettings.BaseUrl | Url til den kørende OS2skoledata Core |
| OS2skoledataSettings.ApiKey | API-nøgle til den kørende OS2skoledata Core |
| AppleSchoolManagerSettings.Domain | Domænenavnet (bruges til email på brugere) |
| AppleSchoolManagerSettings.ZipFileName | Navn på zipfilen, der uploades til Apple |
| AppleSchoolManagerSettings.SFTP.Url | URL til SFTP |
| AppleSchoolManagerSettings.SFTP.Username | Brugernavn til SFTP |
| AppleSchoolManagerSettings.SFTP.Password | Kodeord til SFTP |

Projektet kan bygges fra Visual Studio ved at trykke ”Build” 🡪 ”Build Solution”. Projektet kan køres fra Visual Studio ved at trykke på den grønne pil (start) i topbaren.
Der er også mulighed for at køre en dryRun, hvor filerne bare gemmes på computeren, servicen køres fra.

## SQL sync (on-premise)

SQL sync’en er lavet i c# dotnet 6. Projektet kræver en MariaDB eller MySQL database, som alt data gemmes i. Det henter også data fra OS2skoledata, så en kørende OS2skoledata Core er krævet.

Projektet kan køres fra Visual Studio eller der kan bygges en installer. Se afsnit ”2.3 Active Directory integration” for beskrivelse af hvordan en installer bygges.

## Lønkontrol (on-premise)

Lønkontrol er lavet i c# dotnet 6. Projektet henter data fra OS2skoledata, så en kørende OS2skoledata Core er krævet. Derudover kræves en OPUS fil, en database med lønforhold eller en forbindelse til OS2sofd, for at hente information om aktive ansættelser.

Projektet kan køres fra Visual Studio eller der kan bygges en installer. Se afsnit ”2.3 Active Directory integration” for beskrivelse af hvordan en installer bygges.

# Jobs

Alle integrationer i OS2skoledata køres via automatiske jobs. OS2skoledata Core har et job, der som standard kører en gang om dagen, der henter data ud fra STIL via WS17 og gemmer i databasen. Alle integrationer har skemalagte fulde syncs, der som standard køre en gang om dagen. Det anbefales at integrationernes sync tidspunkt er efter OS2skoledata Core STIL sync. Integrationerne Active Directory, Google Workspace og Azure AD har også skemalagte delta sync tidspunkter. Delta sync kører som standard hvert femte minut, men man kan sagtens køre den sjældnere, da der som OS2skoledata er nu, kun sker ændring i data, når der synkroniseres fra STIL.

Det er muligt at tilpasse tidspunkter for alle jobs.
