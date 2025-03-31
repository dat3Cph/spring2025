---
title: HDJ
description: Her dumper jeg!!!
layout: default
nav_order: 8
parent: Backend
grand_parent: Exam
permalink: /exam/backend/hdj
---

# "Her-Dumper-Jeg" (HDJ)

Følgende er en liste over vigtige ting, som vi gennem årene har erfaret at studerende enten glemmer eller ikke har styr på, når de skal til eksamen. Listen er ikke udtømmende,

![HDJ](../../jpa_part1/exercises/images/hdj.png)

## JPA

1. Husk at annotere dine klasser med `@Entity` og `@Id` på dine primære nøgler.
2. Husk at indsætte dine entitetklasser i `HibernateConfig`-klassen.
3. Husk at annotere dine relationer med `@OneToMany`, `@ManyToOne`, `@OneToOne` og `@ManyToMany`.
4. Husk at undgå cirkulære referencer i dine klasser.
5. Husk at lave hjælpemetoder til at indsætte bi-directionelle relationer.
6. Husk at bruge `CascadeType` i dine relationer - og brug det med omtanke. Dvs, at du ikke nødvendigvis skal bruge `CascadeType.ALL`.
7. Overvej om du skal have FetchType.EAGER eller FetchType.LAZY i dine relationer.
