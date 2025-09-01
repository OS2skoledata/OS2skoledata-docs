---
title: GW opsætning
layout: default
parent: Opsætning
nav_order: 2
has_children: false
---

# Indledning

Dette dokument beskriver hvordan man opretter et projekt i Google Workspace, og giver de fornødne rettigheder, til at OS2skoledata kan integrere med API'erne på Google Workspace, og administrere brugere, enheder og fællesdrev

# Forudsætninger

## Adgang til Admin SDK'et

Det er en forudsætning at man anvender Google Workspace for Education, og har mulighed for at slå Admin SDK'et til.

## Dedikeret brugerkonto

EDIT 08/07/2024: Under første brugerkørsel i Odense, hvor vi ikke havde en super admin, men bare nedenstående roller, fandt vi ud af at opdatering af andre admin konti fejlede. Vores konto blev lavet om til super admin, og problemet forsvandt. Det er ikke lykkes endnu, at finde en alternativ rolle, så indtil videre skal der anvendes en super admin.

\"Delegated admins can\'t update other delegated or super admins.\"[^1]

Der skal oprettes en brugerkonto, der som minimum har følgende roller:

- Organizational units (Read, Create, Update, Delete)

- Users (Read, Create, Update, Delete)

- Groups

- Schema Management (API privilegie)

men det kan også være en superadministrator. Denne konto skal anvendes af integrationen, og bør ikke bruges til andet.

Man skal sørge for at brugeren har lov til at logge ind i Google Cloud Console fx ved at placere den i den enhed, hvor man har andre administratorer, hvis man styrer rettighederne på enheden. Google Cloud Platform service og her under oprettelse af projekter skal være slået til for brugeren.

Bemærk at man med fordel kan logge ind som denne brugerkonto når man skal opsætte rettigheder m.m., da det gør dele af opsætningen nemmere.

# Opsætning af projekt og rettigheder

Start med at logge på Google Cloud konsollen med den oprettede brugerkonto som skal afvikle OS2skoledata integrationen. Accepter evt vilkår m.m. som Google præsenterer, for at sikre at kontoen er klar til brug.

Vælg projekt oppe i den blå top-bar, og på listen over projekter vælges "New Project" for at oprette et nyt projekt som vist nedenfor. Sørg for at skolens domæne er forvalgt

![Graphical user interface, application Description automatically generated](/assets/gw_3_1.png)

På siden der kommer frem, navngives projektet, og der trykkes "Create".

![Graphical user interface, text, application, email Description automatically generated](/assets/gw_3_2.png)

Vælg det oprettede projekt og udfør de næste handlinger under dette.

## Enable Admin SDK, Google Drive API og Google Classroom API

Admin SDK'et enables inde fra Google Cloud konsollen på følgende måde

Gå til <https://console.cloud.google.com/> og vælg "APIs & Services"

![Graphical user interface, application Description automatically generated](/assets/gw_3-1_1.png)

Klik her på "ENABLE APIS AND SERVICES" for at foretage en søgning

![Graphical user interface, text, application, chat or text message Description automatically generated](/assets/gw_3-1_2.png)

Lav her en søgning efter Admin SDK'et, og klik på det og vælg at slå API'et til.

![Graphical user interface, text, application, email Description automatically generated](/assets/gw_3-1_3.png)

Tilsvarende skal Google Drive API aktiveres på præcis samme måde.

Hvis OS2skoledata skal bruges til at overdrage og arkivere Classrooms, skal

Google Classroom API også enables.

## Oprette adgangsnøgler

Vælg "APIs & Services" og herunder "Credentials"

![Graphical user interface, text, application Description automatically generated](/assets/gw_3-2_1.png)

Herunder trykkes på "Create Credentials" og "Service Account"

![Graphical user interface, text, application, email Description automatically generated](/assets/gw_3-2_2.png)

Servicekontoen gives et navn, og der vælges rollen "owner"

![Graphical user interface, text, application, email Description automatically generated](/assets/gw_3-2_3.png)

Forsæt til afslutningen af oprettelsen (ingen yderligere roller er nødvendige) servicekontoen er nu klar. Ude på forsiden klikkes på den oprettede servicekonto som vist nedenfor

Og på fanen "Keys" vælges "Add Key" og herunder "Create new key". Formatet JSON vælges, og workspace danner en ny nøgle, som automatisk downloades som en JSON fil på maskinen. Denne fil skal bruges af OS2skoledata integrationen sammen med brugernavnet på den konto der er oprettet som superadminsitrator (JSON filen indeholder nøgler der bruges til at kalde API'et på vegne af denne brugerkonto).

![Graphical user interface, text, application Description automatically generated](/assets/gw_3-2_4.png)

## Tildele rettigheder

Google Workspace arbejder med såkaldte "scopes" for de data og funktioner som man får adgang til. Dette håndteres ved at oprette en adgang på hele domænet for de nødvendige scopes. Gå til fanen "Details" på den oprettede servicekonto og fold fanen "Advanced settings" ud som vist nedenfor

![Graphical user interface, text, application Description automatically generated](/assets/gw_3-3_1.png)

Noter det "Client ID" der står på siden, og gå så til google admin konsollen, enten ved at klikke på linket, eller ved at gå til

<https://admin.google.com>

Log ind med den oprettede brugerkonto og gå til "Security" -\> "Access and data control" -\> "API controls"

![Graphical user interface, text, application, chat or text message Description automatically generated](/assets/gw_3-3_2.png)

Her vælges "Manage Domain Wide Delegation"

![Graphical user interface, text, application Description automatically generated](/assets/gw_3-3_3.png)

Og endeligt klikkes på "Add new" som vist nedenfor

![Graphical user interface, text, application Description automatically generated](/assets/gw_3-3_4.png)

Her udfyldes skærmbilledet med ID'et fra Google Cloud konsollen (kopieret i tidligere skridt), og listen med Scopes udfyldes med følgende værdier, som giver adgang til hhv brugere, licenser, grupper, enheder og fællesdrev (og klik på "Authorize" for at afslutte)

- https://www.googleapis.com/auth/drive

- https://www.googleapis.com/auth/admin.directory.user

- https://www.googleapis.com/auth/admin.directory.orgunit

- https://www.googleapis.com/auth/admin.directory.group

- <https://www.googleapis.com/auth/apps.licensing>

- <https://www.googleapis.com/auth/admin.directory.userschema>

- <https://www.googleapis.com/auth/classroom.rosters> (hvis det skal være muligt at overdrage og arkivere classrooms)

- <https://www.googleapis.com/auth/classroom.courses> (hvis det skal være muligt at overdrage og arkivere classrooms)

- <https://www.googleapis.com/auth/apps.groups.settings> (hvis OS2skoledata skal håndtere grupperettigheder)

![Graphical user interface, text, application Description automatically generated](/assets/gw_3-3_5.png)

Kontoen er nu klar til brug, og kan kalde Admin SDK API'et med de opsatte scopes for hele domænet.

## Kendte fejlscenarier

### Rettighedsfejl ved håndtering af fællesdrev

Hvis håndtering af fællesdrev fejler med en rettighedsfejl, kan det være, at det skyldes at den OU, hvor vores servicekonto ligger, ikke har rettigheder til at oprette drev. Tjek det sådan her:

apps -\> drive and docs -\> sharingsettings -\> shared drive creation -\> prevent users i ou

[^1]: <https://groups.google.com/g/google-apps-manager/c/zjt3kXwAaOA>
