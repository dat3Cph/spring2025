---
title: Hotel API part 1
description: Hotel API part 1
layout: default
nav_order: 6
grand_parent: Rest API intro
parent: Exercises
has_children: false
permalink: /rest-intro/exercises/hotel-api-part-1/
---

# Exercise with Javalin and CRUD

![Hotel California](./images/hotel_california.jpeg){: .mx-auto .d-block .my-5 .md .d-md-none }
![Hotel California](./images/hotel_california.jpeg){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right}

## Part 1 setup project

- Setup a new maven project in IntelliJ (or use your intellij template with Hibernate)
- Add the following dependencies to the pom.xml file:
  - Javalin
  - JUnit
  - Rest Assured
  - Hamcrest
  - Jackson
  - hibernate
  - postgresql
  - slf4j-api
  - logback
- Create a new javalin application with 2 ressources: `Hotel`  and `Room`
- Create a new database in postgresql called `hotel`
- Create DTOs for `Hotel` and `Room`
  - HotelDTO: id, name, address, rooms
  - RoomDTO: id, hotelId, number, price
- Implement functionality to convert between DTOs and Entities. Both ways.
- Implement an interface with the following methods:
  - getAllHotels()
  - getHotelById()
  - createHotel()
  - updateHotel()
  - deleteHotel()
  - addRoom(Hotel hotel, Room room)
  - removeRoom(Hotel hotel, Room room)
  - getRoomsForHotel(Hotel hotel)

## Part 2 create API Ressources

- Create a HotelController and a RoomController that handles the above functionality using the DTOs
- Create a new Routes.java file that contains all routes for the application and implement the following routes with json:
  - GET /hotel
    - response json: `[{id: 1, name: "Hotel 1", address: "Address 1"}, {id: 2, name: "Hotel 2", address: "Address 2"}]`
  - GET /hotel/{id}
    - response json: `{id: 1, name: "Hotel 1", address: "Address 1"}`
  - GET /hotel/{id}/rooms
    - response json: `[{id: 1, hotelId: 1, number: 1, price: 100}, {id: 2, hotelId: 1, number: 2, price: 200}]`
  - POST /hotel
    - request json: `{name: "Hotel 3", address: "Address 3"}`
    - response json: `{id: 3, name: "Hotel 3", address: "Address 3"}`
  - PUT /hotel/{id}
    - request json: `{name: "Hotel renamedHotel", address: "Address 1"}`
    - response json: `{id: 1, name: "Hotel renamedHotel", address: "Address 1"}`
  - DELETE /hotel/{id}
    - response json: `{id: 1, name: "Hotel 1", address: "Address 1"}`

In above api, if no request json is specified, then the request body should be empty and an appropriate status code should be used.

- Use an http file to test the endpoints.

## Part 3 Error handling

- Implement app.exception() to handle:
  - IllegalStateException: When posting or updating a hotel or room with incorrect json representation.
  - Exception: when anything else goes wrong.

## Part 4: Rest Assured Testing
Setup a rest assured test for the Hotel API. Make The test should test the following:
- Get all hotels
- Get a specific hotel
- Get all rooms for a specific hotel
- Create a new hotel
- Update a hotel
- Delete a hotel

## Part 5: (Optional) logging

Use our small tutorial from yesterday and use LogBack to log requests, responses, and exceptions.

- Implement logging for all requests and responses
- Include the following information in the log:
  - Timestamp
  - Request method
  - Request path
  - Request body
  - Response status code
  - Response body