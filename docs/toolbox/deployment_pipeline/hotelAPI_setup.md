---
title: HotelAPI Setup
description: Deployment Exercises HotelAPI Setup
layout: default
nav_order: 4
grand_parent: Toolbox
parent: Deployment Pipeline
permalink: /toolbox/deployment-pipeline/hotelapi-setup/
---

![Postgres Logo](./images/javalin_logo.png){: .mx-auto .d-block .my-5 .md .d-md-none  style="width: 25%;"}
![Postgres Logo](./images/javalin_logo.png){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right style="width: 25%;"}

# Hotel API and Javalin Setup

In this exercise, you will learn how to set up the HotelAPI Javalin application on your Digital Ocean Droplet. We will pull the image from Docker Hub and launch the Jetty webserver in a Docker Container. We will also make sure that it can connect to the Postgres database that we set up in the previous exercise.

## Introduction - flashback to 2nd semester

To deploy a Javalin + Thymeleaf multipage application, we created a Dockerfile and a docker-compose file and ran the application in a Docker container. We also set up a reverse proxy with Caddy to serve the application over HTTPS and a domain name. You should have a `docker-compose.yml` file on your Droplet in the `~jetty/deployment` folder.

![RedBlue](./images/redblue.webp)

So to sum it up. Your Droplet contains:

Postgres, Caddy, and Javalin configured in the docker-compose.yml file in the `~jetty/deployment` folder. You will probably also have a deployed version of your Carport project etc.

We don't want to mess with the Postgres data, so we keep the `~jetty/deployment` folder as it is and then add to the docker-compose file.

## Step 1: Add the hotelAPI Service to the Docker Compose File

1. Navigate to the `~jetty/deployment` folder on your Droplet.
2. Open the `docker-compose.yml` file in an editor (nano).
3. Add this services to the file below the Postgres service. Remember to rename the image to you own name instead of `jonbertelsen/hotel_api:latest`:

```yml
  hotelAPI:
    image: jonbertelsen/hotel_api:latest
    container_name: hotelAPI
    ports:
      - "7070:7070"
    environment:
      - DEPLOYED=${DEPLOYED}
      - DB_NAME=${DB_NAME}
      - DB_USERNAME=${DB_USERNAME}
      - DB_PASSWORD=${DB_PASSWORD}
      - CONNECTION_STR=${CONNECTION_STR}
      - SECRET_KEY=${SECRET_KEY}
      - ISSUER=${ISSUER}
      - TOKEN_EXPIRE_TIME=${TOKEN_EXPIRE_TIME}
    networks:
      - backend
      - frontend
    volumes:
      - ./logs:/logs
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:7070/api/auth/healthcheck"]
      interval: 30s
      timeout: 5s
      retries: 5
      start_period: 10s

volumes:
  logs:

networks:
  backend:
    name: backend
  frontend:
    name: frontend
```

Notice the healthcheck. It will check if the application is running by calling the `/api/auth/healthcheck` endpoint every 30 seconds. If the application does not respond within 5 seconds, it will retry 5 times with a 10 second start period. This is a good way to make sure that the application is running and healthy. You will need to implement a healthcheck endpoint in your application. We have already done that for you in the HotelAPI. Look in the [`SecurityController`](https://github.com/jonbertelsen/hotel_api_deployable/blob/b7c397b56559ad51ec6f070aa6ecd4fb49892099/src/main/java/dat/security/controllers/SecurityController.java#L194-L197) class, and also, notice the endpoint added in the [`SecurityRoutes`](https://github.com/jonbertelsen/hotel_api_deployable/blob/b7c397b56559ad51ec6f070aa6ecd4fb49892099/src/main/java/dat/security/routes/SecurityRoutes.java#L22).

4. Add the following environment variables to the `.env` file:

   ```properties
   DEPLOYED=true
   DB_NAME=hotel
   DB_USERNAME=postgres
   DB_PASSWORD=<your secure password>
   CONNECTION_STR=jdbc:postgresql://db:5432/
   SECRET_KEY=4c9f92b04b1e85fa56e7b7b0a34f2de4f5b08cd9bb4dfe8ac4d73b4f7f6ef37b
   ISSUER=Bilbo Baggins
   TOKEN_EXPIRE_TIME=18000
   ```

5. Save the file and exit the editor.

## Step 2 Start the Postgres and hotelAPI Services

1. Do this:

    ```bash
    docker compose down
    docker compose up
    ```

    Notice that we left out  the `-d` flag. This is because we want to see the output from the services. If there are any errors, we want to see them. Press Ctrl + C to stop the services.

2. Check that the services are running:

    Log into your droplet with another terminal window and run:

    ```bash
    docker ps
    ```

    You should see the `db` and the `hotelAPI` service running. The `hotelAPI` service might take a little while to get started, since we need to pull the image from Docker Hub. Also, remember to check the logs from the services if you see any errors. One typical error is that the `hotel` database does not exist. You can create it with the following command:

    ```bash
    docker exec -it db psql -U postgres -c "CREATE DATABASE hotel;"
    ```

    Or do it with pgAdmin from your local machine.

## Next step

The next step is to setup [Caddy Server](./caddy_setup.md) to serve the HotelAPI over HTTPS.
