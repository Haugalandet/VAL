# VAL Application Design Document

> [!NOTE]
> This design documentation is WIP,
> and contains information that may or may not be correct.

## Table of Contents

- [Introduction](#1-introduction)

  - [Purpose](#purpose)
  - [Scope](#scope)
  - [Target Audience](#target-audience)
  - [Overview](#overview)

- [Application Components](#2-application-components)

  - [Frontend](#frontend)
  - [Backend](#backend)
  - [RabbitMQ Application](#rabbitmq-application)
  - [Metaend Backend](#metaend-backend)
  - [Metaend Frontend](#metaend-frontend)
  - [IOT Application](#iot-application)

- [Functional Requirements](#3-functional-requirements)

  - [User Registration and Authentication](#user-registration-and-authentication)
  - [Poll Creation and Management](#poll-creation-and-management)
  - [Voting on Polls](#voting-on-polls)
  - [Integration with IOT Devices](#integration-with-iot-devices)
  - [Poll Open and Close Events](#poll-open-and-close-events)
  - [Metadata Display](#metadata-display)

- [Implementation Details](#4-implementation-details)

  - [Frontend (React)](#frontend-react)
  - [Backend (Spring Boot)](#backend-spring-boot)
  - [RabbitMQ Application (Java)](#rabbitmq-application-java)
  - [Metaend Backend (Rust with Actix)](#metaend-backend-rust-with-actix)
  - [Metaend Frontend (Haskell)](#metaend-frontend-haskell)
  - [IOT Application (Rust)](#iot-application-rust)

- [Data Schema](#5-data-schema)

  - [SQLite Database](#sqlite-database)
  - [MongoDB Database](#mongodb-database)

- [Integration Technologies](#6-integration-technologies)

  - [Docker](#docker)
  - [Kubernetes](#kubernetes)

- [Security Measures](#7-security-measures)
  - [Password Hashing](#password-hashing)
  - [User Authentication](#user-authentication)
  - [Poll Access Control](#poll-access-control)
  - [API Security](#api-security)
  - [Secure Communication](#secure-communication)

## 1. Introduction

### Purpose

The VAL application is a web platform designed for creating and voting on polls. This document outlines the design and architecture of the VAL application, including its various components and functionalities.

### Scope

The VAL application consists of multiple parts, including a React-based frontend, a Spring Boot-based backend, a messaging system using RabbitMQ, a metaend backend and frontend, and an IOT device integration. It also allows both public and registered users to participate in polls, and it can interact with external devices for bulk voting.

### Target Audience

This document is intended for developers, designers, and stakeholders involved in the development and deployment of the VAL application.

### Overview

The VAL application enables users to create and participate in polls. Polls can be open or closed, with open polls accessible to the public, and closed polls requiring user authentication. An IOT device can be connected to a specific poll for bulk voting. The application also posts poll data to dweet.io and provides metadata about polls to interested parties.

## 2. Application Components

## Frontend

    Developed in React
    Allows users to create and vote on polls
    Communicates with the backend for data retrieval and submission

### Backend

    Built with Spring Boot
    Utilizes SQLite for data storage
    Provides API endpoints for user management, poll creation, and voting operations

### RabbitMQ Application

    Monitors dweet.io for poll open and close events
    Sends event notifications to the metaend

### Metaend Backend

    Written in Rust with Actix
    Stores event information received from RabbitMQ in a MongoDB database
    Offers API endpoints for accessing event data

### Metaend Frontend

    Developed in Haskell
    Displays event information stored in the MongoDB database

### IOT Application

    Written in Rust
    Supports two modes: Mock IOT device with GUI and Actual IOT device
    Interfaces with the main application for bulk voting operations

## 3. Functional Requirements

### User Registration and Authentication

    Users can create accounts with securely hashed passwords.
    Authentication is required to access closed polls.

### Poll Creation and Management

    Users can create and manage polls with titles, descriptions, and choices.
    Polls can be opened and closed multiple times.

### Voting on Polls

    Users can vote on open polls.
    Voting is limited to one choice per user.

### Integration with IOT Devices

    IOT devices can be connected to specific polls for bulk voting.
    IOT devices can vote for one of the poll choices and reset vote counters.

### Poll Open and Close Events

    The application posts poll open and close events to dweet.io.
    RabbitMQ monitors these events and sends notifications to the metaend.

### Metadata Display

    Metaend stores event data in a MongoDB database.
    Metaend frontend displays event information to interested parties.

## 4. Implementation Details

### Frontend (React)

    Develop the user interface for voting and poll creation.
    Communicate with the backend to retrieve and submit data.

### Backend (Spring Boot)

    Develop API endpoints for user management, poll creation, and voting.
    Store data in an SQLite database.

### RabbitMQ Application (Java)

    Monitor dweet.io for poll open and close events.
    Send event notifications to the metaend backend.

### Metaend Backend (Rust with Actix)

    Receive event notifications from RabbitMQ.
    Store event data in a MongoDB database.
    Implement API endpoints for accessing event information.

### Metaend Frontend (Haskell)

    Display event information stored in the MongoDB database.

### IOT Application (Rust)

    Implement two modes: Mock IOT device with GUI and Actual IOT device.
    Enable communication with the main application for voting operations.

## 5. Data Schema

### SQLite Database

    Store user account information.
    Save poll details, including title, description, choices, and open/closed status.

### MongoDB Database

    Store event data received from RabbitMQ.

## 6. Integration Technologies

### Docker

    Containerize application components for easy deployment and scaling.

### Kubernetes

    Orchestrate containers for efficient management and scaling of application services.

## 7. Security Measures

### Password hashing

Passwords are securely hashed in the frontend and backend.

### User authentication

User authentication is enforced for accessing closed polls.

### Poll Access Control

Access control mechanisms ensure only authorized users can vote.

### API Security

APIs are secured to prevent unauthorized access.

### Secure Communication

Secure communication protocols are used to protect data in transit.

## 8. Conclusion

This design document provides an overview of the VAL application, its components, functional requirements, implementation details, data schema, integration technologies, and security measures. Further development and deployment will follow this design to ensure a robust and secure application.
