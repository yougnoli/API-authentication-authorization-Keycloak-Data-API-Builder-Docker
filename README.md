# 🔐 Secure API Authentication with Keycloak & Data API Builder (DAB)

This repository contains a complete, Dockerized example demonstrating how to build a secure API using **Keycloak** as an Identity Provider and **Data API Builder (DAB)** to expose data from **SQL Server**.

You'll learn how to implement and test the following authentication flows:

- ✅ **Anonymous Access**  
- 🔑 **Resource Owner Password Credentials Flow**  
- 🤖 **Machine-to-Machine Authentication (Client Credentials Flow)**  
- 🙋 **Delegated Authentication (Authorization Code Flow)**

---

## 🧱 Project Structure

```
project-root/
├─ .env
├─ dab-config.json
├─ docker-compose.yml
├─ DAB/
│   ├─ Dockerfile
│   └─ keycloak.crt
└─ keycloak/
    ├─ certs/
    │   ├─ keycloak.crt
    │   └─ keycloak.key
    └─ Dockerfile
```

---

## 🚀 Getting Started

1. Generate SSL certificates for Keycloak:
   ```bash
   openssl req -x509 -newkey rsa:4096 -days 365 -nodes \
     -keyout keycloak/certs/keycloak.key \
     -out keycloak/certs/keycloak.crt \
     -subj "/CN=keycloak" \
     -addext "subjectAltName=DNS:keycloak"
   ```

2. Copy the certificate into the DAB folder:
   ```bash
   cp keycloak/certs/keycloak.crt DAB/keycloak.crt
   ```

3. Build and start all services:
   ```bash
   docker compose up --build -d
   ```

---

## 🧪 Testing the Setup

- Access Keycloak Admin Console: https://keycloak:8443  
  (Login: `admin`, Password: `admin`)

- Access Data API Builder (DAB) REST endpoint:  
  - Anonymous endpoint: `http://localhost:5000/api/OrdersFree`  
  - Secured endpoint: `http://localhost:5000/api/Orders` (requires JWT)

Use **Postman** to test token generation and attach tokens to access the protected API routes.  
More details in the [Medium article](https://medium.com/@tugnolialessio).

---

## 🧠 Concepts Covered

- Authentication vs Authorization
- JWT, JWS, JWE
- OAuth2 Flows
- OIDC Integration
- HTTPS with self-signed certificates
- Role-based access control via DAB config

---

## 📚 References

- [Keycloak Documentation](https://www.keycloak.org/documentation)
- [Data API Builder](https://github.com/Azure/data-api-builder)
- [OAuth2 Specification](https://oauth.net/2/)
- [JWT.IO](https://jwt.io/)

---

## 🛠 Author

**Alessio Tugnoli**  
📝 Medium: [@tugnolialessio](https://medium.com/@tugnolialessio)

---
