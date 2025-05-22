# Case Study

## ASCII Type Generator

### Fullstack Web Application

#### Architecture Document

**Written by:** Eduardo Aire Torres
**Date:** 2025-05-21

## Table of Contents

- [ASCII Type Generator](#ascii-type-generator)

  - [Background](#background)
  - [Requirements](#requirements)
    - [Functional Requirements](#functional-requirements)
    - [Non-Functional Requirements](#non-functional-requirements)
  - [Executive Summary](#executive-summary)
  - [Overall Architecture](#overall-architecture)
    - [Services](#overall-architecture-services)
    - [Scaling](#overall-architecture-scaling)
    - [Messaging](#overall-architecture-messaging)
  - [Services Drill Down](#services-drill-down)
    - [Logging](#logging)
      - [Role](#logging-role)
      - [Technology Stack](#logging-technology-stack)
      - [Architecture](#logging-architecture)
      - [Implementation Instructions](#logging-implementation)
    - [Receiver](#receiver)
      - [Role](#receiver-role)
      - [Technology Stack](#receiver-technology-stack)
      - [Architecture](#receiver-architecture)
      - [Implementation Instructions](#receiver-implementation)
    - [Handler](#handler)
      - [Role](#handler-role)
      - [Technology Stack](#handler-technology-stack)
      - [Architecture](#handler-architecture)
      - [Implementation Instructions](#handler-implementation)
    - [Info](#info)
      - [Role](#info-role)
      - [Technology Stack](#info-technology-stack)
      - [Architecture](#info-architecture)
      - [Implementation Instructions](#info-implementation)

<h2 id="background">Background</h2>

The ASCII Type Generator is an innovative web application that empowers users to create and share stunning ASCII art lettering and alphabets.

With a user-friendly and intuitive interface, the application ensures that users can effortlessly produce their ASCII art while easily browsing and searching through an extensive collection of creations made by others.

This platform serves a clear purpose: to unleash creativity and allow users to share their ASCII art with the world. It captures the nostalgia of the early days of the internet and emphasizes the distinct art of crafting typography in a bold, unconventional manner.

The application effectively stores all ASCII art created by users, enabling them to search, share, and manage their artworks through a powerful user dashboard.

Users initially have access to 3 artworks and 1 alphabet. However, by opting for a premium creator subscription, they can unlock unlimited possibilities, creating as many artworks and alphabets as they desire.

This document meticulously details the architecture of the application, highlighting the services used, the technology stack, and the comprehensive design of the system.

<h2 id="requirements">Requirements</h2>

<h3 id="functional-requirements">Functional Requirements</h3>

1. Enable users to register, log in, create, edit, and delete ASCII artworks, as well as upload and delete their own ASCII alphabets.
2. Store the artworks and alphabets in a database, and display them to other users with a search feature.
3. Implement a revenue model for the website that allows users to subscribe for unlimited uploads and incorporates advertisements on the site.

<h3 id="non-functional-requirements">Non-Functional Requirements</h3>

1. **Data Volume**: 1.9 GB annually
2. **Load**: Fewer than 100 concurrent requests
3. **Number of Users**: Fewer than 1,000 registered users
4. **Error Handling**: Data loss may occur, but users will be informed to try again (proper error handling is in place)
5. **Service Level Agreement (SLA) Level**: Platinum (fully stateless, easily scalable, logged, and monitored)

<h2 id="executive-summary">Executive Summary</h2>

The ASCII Type Generator is a web application that allows users to create and share ASCII art lettering and alphabets. The application is designed to be user-friendly and intuitive, enabling users to easily create their ASCII art and browse through an extensive collection of creations made by others.

The objective of the application is to create a space where users can have fun and unleash their creativity while sharing their ASCII art with the world.

The main focuses of the application are:

- **User Experience**: The application is designed to be user-friendly and intuitive, ensuring that users can easily create their ASCII art and browse through an extensive collection of creations made by others.
- **Creativity**: The application allows users to unleash their creativity and share their ASCII art with the world in a simple and effective way (just by filling an input for the artwork and uploading a TXT file for the alphabet).
- **Community**: The application creates a space where users can share their ASCII art with the world and browse through an extensive collection of creations made by others.
- **Low Cost**: The application is designed to be low-cost, with a revenue model that allows users to subscribe for unlimited uploads and incorporates advertisements on the site and will help to cover the costs of the application and its scalability.

To achieve these objectives, the application is based on an hexagonal architecture, which allows for better separation of concerns and makes it easier to maintain and scale. The technology stack used for the application is .NET Core for the backend, Entity Framework for the data access layer, and Astro with TypeScript and Tailwind CSS for the frontend. This specific stack will allow us to create a lightweight and fast application that is easy to maintain and scale, besides being a low-cost solution.

![Overall Architecture](../_assets/img/overall-architecture.png)

## Mapping the Components

- Receiver
  - User:
    - User ID
    - Registration date
    - Last update
    - Username
    - Password (hashed)
    - Email
    - Profile picture
    - GitHub
  - The artworks and alphabets are stored in a database as text strings with their metadata.
    - Artworks:
      - Artwork ID
      - User ID
      - Creation date
      - Last update
      - Text
      - Art
    - Alphabets:
      - Alphabet ID
      - User ID
      - Creation date
      - Last update
      - Name
      - Description
      - Alphabet
  - Logging:
    - Request ID
    - Correlation ID
    - User ID
    - Request date
    - Request type
    - Message
- Handler:
  - Register:
    - It creates a new user in the database:
      - It can be done via GitHub without a password and account activation.
      - It can be done via email with a password and account activation.
  - Login:
    - It checks the credentials provided by the user and returns a token to be used in the next requests.
  - Artworks:
    - It processes and validates the text from an input provided by the user:
      - Authentication.
      - Invisible captcha.
      - The text is validated by just accepting ASCII characters.
      - The length of the text is limited to 20 characters.
  - Alphabets:
    - TXT files uploaded by the user:
      - Authentication
      - Invisible captcha
      - Validation:
        - They have only valid ASCII characters.
        - They are TXT files (prevent attacks).
        - They are les than 50kB.
        - They have the alphabet structure.
- Information provider
  - Artworks:
    - User Artworks: It returns the artworks of a user.
    - Latest Artworks: It returns the latest 10 artworks allowing pagination.
    - Artwork by name: It returns the artworks by their name.
    - Artwork by user name: It returns the artworks by their user name.
  - Alphabets:
    - User Alphabets: It returns the alphabets of a user.
    - Alphabets: It returns a catalog with all the alphabets.
    - Alphabet by name: It returns the alphabets by their name.
    - Alphabet by user name: It returns the alphabets by their user name.
- Logger:
  - Logs the requests made by the users to the database.
  - Logs the successful requests to the database.
  - Logs the request errors to the database.

## Choosing Messaging Methods

- Receiver
  - The receiver will be the rest API, it will be the entry point for the users to interact with the system.
  - Rest API is the best option here because it needs to respond to simple request and response messages to map the UI and to handle the user requests and the data.
- Handler
  - The data won't be very big, so transport it through JSON and TEXT request/responses wil be more than enough.
  - It will use JWT tokens to authenticate the users and to authorize the requests.
- Info
  - The UI is the is the info layer, it will be a web application that will be used by the users to create their artworks and alphabets.
- Data store
  - An SQL database will be used to store the data, we need this kind to make easier relations between the artworks, alphabets and users.
  - The database will be hosted in a cloud provider to make it easier to scale and to avoid data loss.
- Logger
  - The system can handle the logs in a database, because of the low volume of data it will be the same as the rest of the system just in a different table.
  - When a message is logged, a notification will be sent to a discord channel to notify the developers about the error.

## Designing the Logging Service

- The logging service will be a microservice that will be responsible for logging the requests made by the users to the database.
- It will record the request ID, correlation ID, user ID, request date, request type and message after every request is made, so it will be injected in the receiver.
- Our receiver will be a rest API written in .NET Core, which will be the entry point for the logging service.

```
-> Polling (it will poll the database to get the logs)
-> Business Logic (it handles the requests and responses and logs the requests)
-> Data Access Layer (it stores the data in the database), we'll use Entity Framework to make it easier to access the database.
```

## Designing the Receiver

- The receiver will be a REST API written in .NET Core exposing the endpoints to handle the requests made by the users.

```
|———————————————————|—————————|
| Service Interface |         |
|———————————————————|         |
| Business Logic    | Logging |
|———————————————————|         |
| Data Access Layer |         |
|———————————————————|—————————|
```

## Designing the Handler

- The handler will validate the requests made by the users and will process the data to be sent to the receiver.
- This will be injected in the receiver as a service, to handle authentication and authorization.
- We'll use JWT tokens to authenticate the users and to authorize the requests.

## Designing the Info Service

- This will be a web application that will be used by the users to create their artworks and alphabets.
- The technology stack will be Astro with TypeScript, and Tailwind CSS.
