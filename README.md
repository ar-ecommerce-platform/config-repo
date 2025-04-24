# Config Repo – E-commerce Backend

This repository stores configuration files for all microservices in the e-commerce backend.  
It works with the Spring Cloud Config Server to deliver the right config values to each service at runtime.

Each environment (like `dev`, `test`, or `prod`) can have its own settings — making it easy to manage configuration in one central place.

--- 
## 📂 Structure

```
ecommerce-config-repo/
├── auth-service-dev.yml
├── discovery-server-dev.yml
├── config-server-dev.yml
├── application.yml  # Common base config
```

- Each microservice gets its own file: `{service-name}-{profile}.yml`
- Profile-specific files (`-dev`, `-test`, `-prod`) enable environment-specific overrides

---

## 🔧 Usage

Services connect to the config server like this:

```yml
spring:
  config:
    import: optional:configserver:http://localhost:8888
```

The config server loads files from this repo and delivers values to the services.

---

## 🔁 Example

To fetch config for auth-service using the dev profile, Spring Cloud will hit:

```
GET http://localhost:8888/auth-service/dev
```

---

## 🔐 Secrets & Security Roadmap

This project is evolving its approach to secrets management. Here's how it's handled across different stages:

### ✅ Right Now (Development)
- Example values (like `authuser` / `authpass`) are stored in config files for local testing
- These are **not real secrets** — just placeholders for dev use

### 🔜 Coming Soon (Staging)
- Move real secrets (like database passwords) out of config files
- Use **Docker Secrets** or `.env` files to pass in sensitive info securely

### 🚀 Future Plans (Production)
- Use a secure tool like **HashiCorp Vault** to store and manage secrets
- Load secrets automatically during deployment using CI/CD
- Add strict access rules and track who accesses what

---

## 🧱 Related Services

- Infrastructure & Core Services
    - [ecommerce-infra](https://github.com/AlexisRodriguezCS/ecommerce-infra) — Infrastructure setup with Docker, CI/CD, ELK logging, Postman, and documentation
    - [ecommerce-config-repo](https://github.com/AlexisRodriguezCS/ecommerce-config-repo) — Git repo for configs **(this repo)**
    - [ecommerce-config-server](https://github.com/AlexisRodriguezCS/ecommerce-config-server) — Centralized configuration service 
    - [ecommerce-discovery-server](https://github.com/AlexisRodriguezCS/ecommerce-discovery-server) — Eureka-based service registry
    - [ecommerce-api-gateway](https://github.com/AlexisRodriguezCS/ecommerce-api-gateway) — API gateway with routing, JWT validation, and rate limiting

- Microservices
    - [ecommerce-auth-service](https://github.com/AlexisRodriguezCS/ecommerce-auth-service) — User authentication and JWT management
    - [ecommerce-product-service](https://github.com/AlexisRodriguezCS/ecommerce-product-service) — Product catalog creation, updates, and search
    - [ecommerce-inventory-service](https://github.com/AlexisRodriguezCS/ecommerce-inventory-service) — Inventory tracking and stock adjustments
    - [ecommerce-order-service](https://github.com/AlexisRodriguezCS/ecommerce-order-service) — Order processing and checkout workflows
    - [ecommerce-payment-service](https://github.com/AlexisRodriguezCS/ecommerce-payment-service) — Secure payment processing
    - [ecommerce-notification-service](https://github.com/AlexisRodriguezCS/ecommerce-notification-service) — Email and SMS notifications for order events

---

## 📬 Contact

Maintained by [Alexis Rodriguez](https://github.com/AlexisRodriguezCS)

---