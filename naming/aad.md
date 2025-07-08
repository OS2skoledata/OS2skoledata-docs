---
title: AAD
layout: default
parent: Navnestandarder
nav_order: 3
has_children: false
---
# Azure Active Directory

## Konfiguration af gruppenavne

| Gruppe type | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| Gruppe til alle i en institution (både elever og medarbejdere) | {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | sikkerhedgruppe_{INSTITUTION_NAME}<br><br>\_{INSTITUTION_NUMBER}\_alle |
| Gruppe til alle elever i en institution | {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | sikkerhedgruppe_{INSTITUTION_NAME}<br><br>\_{INSTITUTION_NUMBER}\_elever |
| Gruppe til alle medarbejdere i en institution | {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | sikkerhedgruppe_{INSTITUTION_NAME}<br><br>\_{INSTITUTION_NUMBER}\_ansatte |
| Gruppe pr klasse | {CLASS_NAME}, {CLASS_ID}, {CLASS_LEVEL}, {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | sikkerhedgruppe_klasse<br><br>\_{CLASS_NAME}\_{CLASS_ID}<br><br>\_{CLASS_LEVEL}\_{INSTITUTION_NAME}<br><br>\_{INSTITUTION_NUMBER}\_alle |
| Gruppe pr år i en institution. Grupperne ændrer sig aldrig, men eleverne ændrer sig | {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION},{LEVEL} | {INSTITUTION_NAME} {LEVEL}. klasse |
| Alle medarbejdere i hele kommunen |     | alle_ansatte |
| Alle elever i hele kommunen |     | alle_elever |
| Gruppe pr år i hele kommunen. Grupperne ændrer sig aldrig, men eleverne ændrer sig | {LEVEL} | {LEVEL}. klasse |

## Konfiguration af teams

| Team type | Mulige pladsholdere | Eksempel |
| --- | --- | --- |
| Navn på Team til alle medarbejdere i en institution | {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | {INSTITUTION_NAME}-medarbejdere |
| Email på Team til alle medarbejdere i en institution | {INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | {INSTITUTION_NAME}-medarbejdere |
| Navn på Team pr klasse | {CLASS_NAME},<br><br>{CLASS_ID},<br><br>{CLASS_LEVEL},<br><br>{CLASS_YEAR},<br><br>{INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION}, {INSTITUTION_NUMBER} | {CLASS_NAME}-{INSTITUTION_NAME}-team |
| Email på Team pr klasse | {CLASS_NAME},<br><br>{CLASS_ID},<br><br>{CLASS_LEVEL},<br><br>{CLASS_YEAR},<br><br>{INSTITUTION_NAME},<br><br>{INSTITUTION_ABBREVIATION},<br><br>{INSTITUTION_NUMBER},<br><br>{CLASS_DATABASE_ID} | {CLASS_YEAR}{CLASS_LINE}-{INSTITUTION_NAME}-team |