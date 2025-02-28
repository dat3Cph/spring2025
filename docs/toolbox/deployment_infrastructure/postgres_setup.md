---
title: 6. Postgres
description: Opsætning Postgres på Droplet
layout: default
grand_parent: Toolbox
parent: Deployment Infrastructure
permalink: /toolbox/deployment-infrastructure/postgres-setup
nav_order: 7
---
# Opsætning af Postgres i en Docker container på en Droplet

Vi har allerede oprettet en Droplet med Ubuntu og Docker hos Digital Ocean. Ideen er nu
at vi skal have Postgres til at køre i en container. Og mere specifikt - den samme version,
som kører lokalt på vores laptops. Det kræver blot at vi kloner, tilpasser og eksekverer en `docker-compose.yml` fil fra Github. Vi skal være omhyggelige med at vælge et godt password til Postgres, så ikke vi bliver hacket. Følg nedenstående vejledning:

1. Log ind på din droplet som `jetty` og stå i din hjemme folder `~jetty`
2. Klon denne docker-compose.yml fil:

```bash
git clone https://github.com/dat2Cph/2semDockerSetupRemote.git
```

Hop ned i folderen `2semDockerSetupRemote`:

```bash
cd 2semDockerSetupRemote
ls
```

3. Følg instruktionerne i [README](https://github.com/dat2Cph/2semDockerSetupRemote) filen. Du skal sætte `sudo` foran kommandoerne

## Videre herfra

- [Næste trin](./snapshot.md)
- [Hop tilbage til oversigten](./README.md)
