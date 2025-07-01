---
title: GW
layout: default
parent: Navnestandarder
nav_order: 2
has_children: false
---
# Google Workspace

## Konfiguration af gruppenavne

| Gruppe type | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| Gruppe til alle i en institution (både elever og medarbejdere) | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_alle |
| Gruppe til alle elever i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_elever |
| Gruppe til alle medarbejdere i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_ansatte |
| Gruppe pr klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_{CLASS_NAME}\_{CLASS_YEAR}\_alle |
| Gruppe til elever pr klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_{CLASS_NAME}\_{CLASS_YEAR}\_elever |
| Gruppe pr type af ansat i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER},<br>{TYPE} | {INSTITUTION_NAME}\_alle_{TYPE} |
| Gruppe pr år i en institution. Grupperne ændrer sig aldrig, men eleverne ændrer sig | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{LEVEL} | {INSTITUTION_NAME} {LEVEL}. klasse |
| Alle medarbejdere i hele kommunen | *(ingen)* | alle_ansatte |
| Gruppe pr år i hele kommunen. Grupperne ændrer sig aldrig, men eleverne ændrer sig | {LEVEL} | {LEVEL}. klasse |
| Gruppe til elever pr klasse pr skoleår (bruges til mappe i fællesdrev) | {SCHOOL_YEAR} (påkrævet),<br>{CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {SCHOOL_YEAR} {INSTITUTION_NAME} {CLASS_NAME} |

---

## Konfiguration af drev

| Drev type | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| Drev til alle medarbejdere i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME} - medarbejdere |
| Drev pr klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{INSTITUTION_NAME},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}-{CLASS_NAME}-{CLASS_YEAR} - alle |
| Drev til institutionen hvori der oprettes klassemapper | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME} |

---

## Konfiguration af mapper i fællesdrev

| Mappe type | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| Mappe pr klasse pr skoleår | {SCHOOL_YEAR} (påkrævet),<br>{CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {SCHOOL_YEAR} {CLASS_NAME} |

---

## Konfiguration af enhedsnavne

| Enhedstype | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| OU til medarbejdere under hver institution | *(ingen)* | medarbejdere |
| OU til elever under hver institution | *(ingen)* | elever |
| OU til elever, der ikke er tilknyttet klasser, under hver institution | *(ingen)* | elever udenfor grupper |
| OU pr klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{CLASS_LINE},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_{CLASS_YEAR}\_{CLASS_LINE} |
| OU pr institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME} ({INSTITUTION_NUMBER}) |
| Navn på den OU hvor alle institutioner af typen skole placeres under | *(ingen)* | skoler |
| Navn på den OU hvor alle institutioner af typen daginstitutioner placeres under | *(ingen)* | daginstitutioner |
| Navn på den OU hvor alle institutioner af typen FU/klubber placeres under | *(ingen)* | fu |
