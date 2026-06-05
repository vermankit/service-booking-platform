# UrbanClap-Like Service Provider Platform - Microservices POC

## Overview

This project is a Proof of Concept (POC) for an UrbanClap-style service provider platform built using a microservices architecture. The system enables customers to book services, partners to provide services, and administrators to manage bookings and assignments.

## Architecture Diagram

![Architecture Diagram](https://user-images.githubusercontent.com/17446840/142975748-e7355a2f-9250-4440-8d87-8d88f27f2193.jpg)

## API Gateway

All services communicate through the API Gateway and are discoverable via Eureka Service Discovery.

### Gateway Endpoints

| Service | Endpoint |
|----------|----------|
| Booking Service | http://localhost:7000/booking |
| Admin Service | http://localhost:7000/admin |
| Partner Service | http://localhost:7000/partner |
| Customer Service | http://localhost:7000/customer |

### Internal Service Endpoints

| Service | URL |
|----------|----------|
| Consumer Provider | http://localhost:5001/api |
| Notification Provider | http://localhost:5002/api |
| Partner Provider | http://localhost:5003/api |
| Gateway | http://localhost:7000 |

---

## Microservices

### 1. Partner Service

The Partner Service is responsible for managing service providers such as cleaners, cooks, electricians, and other professionals.

#### Responsibilities

- Register new service providers.
- Retrieve partner information by email.
- Retrieve partners based on area code.
- Maintain partner-related information.

---

### 2. Booking / Admin Service

The Booking Service manages customer bookings and booking workflows.

#### Responsibilities

- Accept booking requests from customers.
- Allow administrators to assign bookings to partners.
- Allow partners to approve or reject assigned bookings.
- Retrieve customer and partner details through synchronous HTTP communication.

---

### 3. Consumer Service

The Consumer Service manages customer information.

#### Responsibilities

- Maintain customer profiles.
- Provide customer details to the Booking Service.
- Support customer-related operations.

---

### 4. Email Notification Service

The Notification Service is responsible for sending email notifications to customers and partners.

#### Responsibilities

- Send booking assignment notifications to partners.
- Send booking confirmation notifications to customers.
- Integrate with an email server for message delivery.

#### Email Content

**Partner Notification**

Contains customer and booking details required for fulfilling the service.

**Customer Notification**

Contains booking confirmation details along with assigned partner information.

---

## Alternative Notification Approach

Instead of using email notifications, real-time notifications could be implemented using SignalR.

### Benefits of SignalR

- Real-time communication
- Instant booking updates
- Improved user experience
- Reduced dependency on email delivery

---

## Technology Highlights

- Microservices Architecture
- API Gateway Pattern
- Service Discovery (Eureka)
- REST APIs
- Synchronous Inter-Service Communication
- Email Notifications
- SignalR (Alternative Notification Strategy)

---

# Running the Application

## Prerequisites

- Docker
- Visual Studio 2022 (or later)
- .NET SDK

## Step 1: Start RabbitMQ

Run the following command to start RabbitMQ with the Management UI enabled:

```bash
docker run -it --rm --name rabbitmq \
-p 5672:5672 \
-p 15672:15672 \
rabbitmq:3.12-management
```

RabbitMQ Management UI will be available at:

- URL: http://localhost:15672
- Username: `guest`
- Password: `guest`

## Step 2: Configure Startup Projects

Open the solution in Visual Studio and configure all required projects as startup projects:

1. Right-click the solution in **Solution Explorer**.
2. Select **Properties**.
3. Navigate to **Startup Project**.
4. Choose **Multiple Startup Projects**.
5. Set all required projects to **Start**.

## Step 3: Run the Backend Services

Press **Ctrl + F5** to start all backend services without debugging.

## Verify the Application

- Ensure all backend services start successfully.
- Verify that RabbitMQ is running by opening http://localhost:15672.
- Check the application logs for any startup errors.
