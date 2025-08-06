---
title: AD
layout: default
parent: Navnestandarder
nav_order: 1
has_children: false
---

# Active Directory

## Konfiguration af gruppenavne

| Gruppe type | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| Gruppe til alle i en institution (både elever og medarbejdere) | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_alle |
| Gruppe til alle elever i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_elever |
| Gruppe til alle medarbejdere i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_ansatte |
| Gruppe pr klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{CLASS_LINE},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | {INSTITUTION_NAME}\_{CLASS_YEAR}\_{CLASS_LINE} |
| Gruppe til alle elever i en klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{CLASS_LINE},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | elever_{INSTITUTION_NAME}\_{CLASS_YEAR}\_{CLASS_LINE} |
| Gruppe til alle medarbejdere knyttet til en klasse | {CLASS_NAME},<br>{CLASS_ID},<br>{CLASS_LEVEL},<br>{CLASS_YEAR},<br>{CLASS_LINE},<br>{INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER} | medarbejdere_{INSTITUTION_NAME}\_{CLASS_YEAR}\_{CLASS_LINE} |
| Gruppe pr type af ansat i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_NUMBER},<br>{TYPE} | {INSTITUTION_NAME}\_alle_{TYPE} |
| Gruppe pr årgang i en institution | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{INSTITUTION_NUMBER},<br>{YEAR} | {INSTITUTION_NAME}\_elever_år\_{YEAR} |
| Gruppe pr år i en institution. Grupperne ændrer sig aldrig, men eleverne ændrer sig | {INSTITUTION_NAME},<br>{INSTITUTION_ABBREVIATION},<br>{LEVEL} | {INSTITUTION_NAME} {LEVEL}. klasse |
| Gruppe pr type af ansat på tværs af daginstitutioner | {TYPE} | alle_{TYPE}\_daginstitutioner |
| Gruppe pr type af ansat på tværs af skoler | {TYPE} | alle_{TYPE}\_skoler |
| Gruppe pr type af ansat på tværs af FU/Klubber | {TYPE} | alle_{TYPE}\_fu |
| Alle medarbejdere i hele kommunen | *(ingen)* | alle_ansatte |
| Alle elever i hele kommunen | *(ingen)* | alle_elever |
| Gruppe pr år i hele kommunen. Grupperne ændrer sig aldrig, men eleverne ændrer sig | {LEVEL} | {LEVEL}. klasse |

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
