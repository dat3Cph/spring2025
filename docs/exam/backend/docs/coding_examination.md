---
title: Coding Examination
description: Help for the coding examination
layout: default
nav_order: 9
nav_exclude: false
search_exclude: false
parent: Backend
grand_parent: Exam
permalink: /exam/backend/coding-examination
---

# Kode eksamen - emneoversigt

Kære alle

For at stille alle ens før den skriftlige eksamen, vil vi kort præcisere hvilke emner,
der potentielt kan dukke op i den skriftlige eksamen.
I har jo fået udleveret to gamle eksamenssæt, som I kan bruge til at øve jer på. Men de dækker
ikke alt, hvad I har lært. Vi lægger også fokus forskellige steder i de
forskellige semestre.

Så i den skriftlige eksamen kan der forekomme følgende emner:

Programmering af et REST API Javalin med:

| **** | **Topic**                                                  | ****                                                                                                                |
|------|------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| 1    | Routes                                                     | We have done many of those in the exercises. [Examples](https://github.com/jonbertelsen/hotel_api_deployable/tree/exceptionhandling/src/main/java/dat/routes)                                                                                                                    |
| 2    | Controllers                                                | We have done many of those in the exercises. [Examples](https://github.com/jonbertelsen/hotel_api_deployable/tree/exceptionhandling/src/main/java/dat/controllers/impl)                                                                                                                    |
| 3    | DAO                                                        | We have done many of those in the exercises. [Examples](https://github.com/jonbertelsen/hotel_api_deployable/tree/exceptionhandling/src/main/java/dat/daos/impl)                                                                                                                    |
| 4    | DTO's                                                      | [Json to dto conversions and more](../../../toolbox/dataintegration/dto_conversion.md)                             |
| 5    | JPA (Hibernate)                                            | [HibernateConfig Example](https://github.com/jonbertelsen/hotel_api_deployable/blob/exceptionhandling/src/main/java/dat/config/HibernateConfig.java)                                                                                                                    |
| 6    | Logging                                                    | [How to use the logger](../../../toolbox/javalin/logging.md)                                               |
| 7    | Exception handling and error messages as json responses    |  [Check the controllers and daos in this branch](https://github.com/jonbertelsen/hotel_api_deployable/tree/exceptionhandling)                                                                                                               |
| 8    | Generics                                                   | [Generics overview](../../../toolbox/java/deepdive/generics.md)                                                                                                                    |
| 9    | Streams                                                    | [Streams overview](../../../toolbox/java/deepdive/streams.md)                                                                                                                    |
| 10   | Fetching json from an external API and parsing it to a DTO | [Fetching from api cookbook](../../../toolbox/dataintegration/httpclient.md)                                             |
| 11   | DAO tests                                                  | [Example](https://github.com/jonbertelsen/gls/blob/main/src/test/java/dat/PackageDAOTest.java). Be careful which version of HibernateConfig you use!                                                                                                                     |
| 12   | Rest Assured tests                                         | [Rest assured overview](../../../toolbox/test/rest_assured.md)                                                                    |
| 13   | Securing Rest Endpoints with JWT and logins                | 1. [Overview of security](../../../toolbox/security/api_security.md)<br/>2. [How to apply security to a project](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Sessions/List.aspx?folderID=7e145a6e-511b-48b0-919f-b20200ef108e) |

## Startkode

Endvidere har vi anbefalet alle at lave en startkode, som I kan bruge til at starte jeres eksamen med. Det letteste er at lave en custom template i IntelliJ. I kan hvor det gøres her:

- [Custom template i IntelliJ](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=7708031b-7a36-4995-8468-b21a01153a70)

## Fejlhåndtering i Javalin (præcisering)

Det blev tydeligt under vores gennemgang af de gamle eksamenssæt, at vi ikke har fået præciseret, hvordan fejlhåndtering skal foregå i Javalin. Derfor vil vi gerne præcisere, at fejlhåndtering skal foregå i en exceptionhandler, som fanger alle exceptions og returnerer et JSON response med en fejlbesked og en statuskode. I kan se et [eksempel på, hvordan dette kan gøres her](https://github.com/jonbertelsen/hotel_api_deployable/tree/exceptionhandling) hvis i kigger i controllers og daos.
Selve exceptionklasserne ligger i `dat.exceptions` pakken, og der hvor de bliver håndteret og pakket ind i et JSON response sættet op i ApplicationConfig. Dvs, at hvis man smider en exception i en controller eller dao, så vil den blive fanget i exceptionhandleren og returnere et JSON response.

Her er en kort videogennemgang af ovenstående, så det forhåbentlig falder på plads:

- [Error and Exceptionhandling i Javalin](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=c39a2112-4b0f-4bae-b911-b21a015de219)
