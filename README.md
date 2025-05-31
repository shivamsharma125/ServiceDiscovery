# 🔍 Service Discovery

The **Service Discovery** microservice is the central registry component in this e-commerce microservices architecture. It uses **Netflix Eureka Server** to allow microservices to dynamically register themselves and discover other services without hard-coded endpoints, enabling scalability, load balancing, and fault tolerance.

---

## 🚀 Key Features

* ✅ Centralized registry for all microservices
* ✅ Enables service-to-service communication without hard-coded URLs
* ✅ Facilitates load balancing and fault tolerance
* ✅ Eureka web dashboard to monitor registered services in real-time

---

## 🛠️ Tech Stack

* Java 17
* Spring Boot 3.x
* Spring Cloud Netflix Eureka Server
* Maven

---

## 🧩 Architecture Overview

```
         +---------------------------+
         |     Eureka Server        |
         |   (Service Discovery)    |
         +-----------+-------------+
                     ^
         +-----------|-----------+
         |           |           |
  +------+---+   +---+------+  +--+-------+
  | Product   |   | User     |  | Payment |
  | Service   |   | Service  |  | Service |
  +-----------+   +----------+  +----------+
         \
          \
      +-----------+
      |  Email     |
      |  Service   |
      +-----------+
```

* Each microservice registers itself with Eureka at startup
* Services query Eureka to discover other services dynamically
* The Eureka dashboard (accessible at `http://localhost:8761`) shows service status

---

## ⚙️ Configuration Highlights

To run the Eureka server:

```properties
spring.application.name=ServiceDiscovery
server.port=8761

# Eureka server should not register itself
# or fetch registry from others

eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

---

## 📡 Eureka Dashboard

Once running, navigate to:

```
http://localhost:8761
```

Here, you can:

* View all registered services
* Monitor their status and availability
* Verify heartbeat and instance metadata

---

## 🔌 Integrating a Client Service

Each client microservice (e.g., Product, User, Email) must:

* Add the dependency: `spring-cloud-starter-netflix-eureka-client`
* Provide configuration:

```properties
# Client application name
spring.application.name=ProductService

# Eureka Server URL
eureka.client.service-url.defaultZone=http://localhost:8761/eureka

# Client should register with Eureka
# and should be able to fetch registry
eureka.client.register-with-eureka=true
eureka.client.fetch-registry=true
```

---

## 📌 Related Microservices

* 📂 **Product Service** – Manage product catalog
* 👤 **User Service** – Handle user registration and authentication
* 📧 **Email Service** – Send transactional emails via Kafka events
* 💳 **Payment Service** – Manage payments via Razorpay & Stripe

---
