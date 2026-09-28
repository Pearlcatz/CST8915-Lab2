# CST8915 Lab 2 - Azure Microservices Deployment

**Student:** Pearl Williams-Cox  

**Student Number:** 040926099

**Course:** CST8915 - Full-stack Cloud-native Development  

**Lab:** Lab 2

---

## Demo Video

[Watch my Lab 2 Demo Video](https://youtu.be/0buAPLPCygY)

---

## Service Repositories

For this lab, I separated the application into three repositories for each of the main services:

- [Order Service](https://github.com/Pearlcatz/CST8915-Lab2-Order-Service)
- [Product Service](https://github.com/Pearlcatz/CST8915-Lab2-Product-Service)
- [Store Front](https://github.com/Pearlcatz/CST8915-Lab2-Store-Front)

---

## Reflection Questions

### 1. What changes did you make to the Order Service and Product Service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?

For the Order Service, I changed the RabbitMQ connection so that it is loaded from an environment variable instead of being hard-coded directly into the application. I used a `.env` file to store the RabbitMQ connection information and used `dotenv` in the application to load it.

For the Product Service, I changed the application so that the port is read from the `PORT` environment variable instead of only being hard-coded as port 3030. I kept 3030 as the default in case the environment variable is not set.

These changes keep the configuration separate from the application code. RabbitMQ is also treated as a backing service because the Order Service connects to it through configuration rather than having the connection information built directly into the source code.

### 2. Why should environment variables be used instead of hard-coded configurations?

Environment variables make it easier to change configuration without having to edit the application's source code. For example, the application could use different ports or RabbitMQ connection information depending on the environment where it is running.

They also help keep sensitive information, such as passwords and connection strings, out of the source code and GitHub repository.

### 3. Why should each microservice have its own repository?

Keeping each microservice in its own repository allows the services to be developed and updated independently. For example, a change to the Product Service does not require changing the Order Service repository.

It also makes the application easier to maintain because each service has its own code, dependencies, version history, and deployment process. This fits the microservices approach because the individual services remain separate instead of being tightly connected together in one large project.

---

## Lab Overview

For this lab, I deployed the application across separate Azure virtual machines. The Store Front communicates with the Product Service to load the available products and sends orders to the Order Service. The Order Service then sends the order to RabbitMQ.

During my demo, I verified the environment variable configurations, loaded the products through the Store Front, placed an order, and confirmed that the RabbitMQ queue message count increased.
