---
title: Konfiguration
layout: default
nav_order: 4
has_children: true
---

# Brugernavnestandarder

Brugernavnestander anvendes når OS2skoledata opretter en ny bruger medmindre brugeren har fået medsendt et reservedUsername.

Hvis en burger har færre tegn i sit fornavn, end der er krævet i brugernavnestandarden, tilføjes der x. For eksempel kunne bo blive til boxx.

## FROM_STIL_OR_AS_UNILOGIN og FROM_STIL_OR_AS_UNILOGIN_RANDOM (anbefales)

Disse brugernavnestandarder tager brugernavnet fra STIL, hvis det er af den gamle type (4 bogstaver fra navnet og 4 tal). Hvis brugernavnet fra STIL er af den nye type (10 random tegn), danner OS2skoledata et brugernavn, der minder om den gamle type fra STIL. FROM_STIL_OR_AS_UNILOGIN danner et brugernavn med de fire første bogstaver fra brugerens fornavn og 4 tal, der starter med 0000, så 0001 osv alt efter hvor mange, der er oprettet med samme fire bogstaver i brugernavnet.  
Når FROM_STIL_OR_AS_UNILOGIN_RANDOM anvendes, er det muligt at konfigurere hvor mange tal og bogstaver, der skal anvendes til at danne brugernavnet. Derudover er det random tal og ikke i rækkefølge som det er med FROM_STIL_OR_AS_UNILOGIN.

Et eksempel på et brugernavn kunne være amal2834

## AS_UNILOGIN

Samme som FROM_STIL_OR_AS_UNILOGIN, men uden at bruge brugernavnet fra STIL. Her dannes altid et nyt brugernavn til brugeren, der skal oprettes.

Et eksempel på et brugernavn kunne være amal0000

## THREE_NUMBERS_THREE_CHARS_FROM_NAME

Her dannes brugernavnet af tre tal og tre bogstaver fra navnet. Tallene 0 og 1 anvendes ikke. Eventuelt brugernavn fra STIL ignoreres.

Et eksempel på et brugernavn kunne være 222ama

## PREFIX_NAME_FIRST og PREFIX_NAME_LAST

Her kan der konfigureres et prefix, der anvendes i starten af alle brugernavne.

Derefter kommer enten tre bogstaver fra navnet eller tre cifre alt efter hvilken af de to standarder der er valgt.

PREFIX_NAME_FIRST kunne fx danne dette brugernavn os2ama2a2({prefix}{tre tegn fra navn}{tre cifre})

PREFIX_NAME_LAST kunne fx danne dette brugernavn os22a2ama({prefix}{tre cifre}{tre tegn fra navn})

Eventuelt brugernavn fra STIL ignoreres.

## UNIID (kun Google Workspace)

Her tages UNIID’et direkte fra STIL uanset om det er ny eller gammel type.

## RANDOM

Her dannes brugernavnet af et konfigurabelt antal random bogstaver og tal. Tallene 0 og 1 og bogstaverne L, l, I, i, O, o, Æ, æ, Ø, ø, Å, å anvendes ikke. Eventuelt brugernavn fra STIL ignoreres.

Et eksempel på et brugernavn kunne være iwty395

# Konfigurationsmuligheder

## Overordnet

Hver enkel integration konfigureres i dens egen kodebase. On-premise integrationernes konfiguration kan ændres af kommunen selv mens de øvrige integrationer kun kan ændres af driftoperatøren.  
Der kan læses mere om navnestandarder i dokumentet ”OS2skoledata navnestandarder”