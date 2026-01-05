# Docker Project – API, Web App & Private Registry

## 📌 Overview

This project demonstrates a complete Docker-based stack including:

* A **Python REST API** exposing student data
* A **PHP web application** consuming the API
* A **private Docker Registry** secured with HTTP Basic Auth (htpasswd)
* A **Docker Registry UI** for image visualization and management
* Orchestration using **Docker Compose**

The goal of this project is to showcase solid Docker fundamentals, container networking, image lifecycle management, and registry operations in a DevOps-oriented context.

---

## 🧱 Project Structure

```text
.
├── docker-compose.yml              # Application stack (API + Web)
├── docker-compose-registry.yml     # Private registry + UI
├── simple_api/                     # Python API
│   ├── Dockerfile
│   ├── student_age.py
│   ├── student_age.json
│   └── requirements.txt
├── website/                        # PHP frontend
│   └── index.php
├── registry/
│   └── auth/
│       └── htpasswd                # Registry credentials
└── README.md
```

---

## ⚙️ Stack Description

### 1️⃣ Python API (`simple_api`)

* Exposes a REST endpoint returning student ages
* Secured with HTTP Basic Auth
* Runs on port **5000**

Example endpoint:

```
GET /pozos/api/v1.0/get_student_ages
```

---

### 2️⃣ PHP Web Application (`website`)

* Simple PHP frontend
* Queries the Python API
* Runs on Apache (port **80** inside container)

---

### 3️⃣ Private Docker Registry

* Based on `registry:2`
* Secured using **htpasswd** authentication
* Exposed on port **5000**

Authentication is mandatory for push/pull operations.

---

### 4️⃣ Docker Registry UI

* Image: `joxit/docker-registry-ui`
* Accessible via browser on port **8080**
* Acts as a **read-only / management UI**
* Proxies requests to the registry

> Note: Browsers may cache HTTP Basic Auth credentials. Use private browsing to re-trigger the authentication popup.

---

## 🚀 How to Run

### ▶️ Application Stack

```bash
docker compose up -d
```

Services started:

* API container
* Web application container

---

### ▶️ Private Registry Stack

```bash
docker compose -f docker-compose-registry.yml up -d
```

Services started:

* Private Docker registry
* Registry UI

---

## 🔐 Registry Authentication

Default credentials:

* **Username:** pozos
* **Password:** pozos

Login from CLI:

```bash
docker login localhost:5000
```

---

## 📦 Image Lifecycle Example

### Tag an image

```bash
docker tag api:v1.0 localhost:5000/api:v1.0
```

### Push to private registry

```bash
docker push localhost:5000/api:v1.0
```

### Verify

```bash
curl -u pozos:pozos http://localhost:5000/v2/_catalog
```

---

## 🌐 Access Points

| Service      | URL                                            |
| ------------ | ---------------------------------------------- |
| API          | [http://localhost:5000](http://localhost:5000) |
| Web App      | [http://localhost:8080](http://localhost:8080) |
| Registry API | [http://localhost:5000](http://localhost:5000) |
| Registry UI  | [http://localhost:8080](http://localhost:8080) |

---

## 🧠 Key DevOps Concepts Demonstrated

* Docker image creation (Dockerfile)
* Container networking (bridge networks)
* Docker Compose orchestration
* Private registry setup
* Registry authentication (htpasswd)
* Reverse proxy usage
* Image push/pull lifecycle
* Debugging ports, auth, and networking issues

---

## 📎 Notes

* Registry data is persisted locally and **must not be committed** to Git
* The `version` field in Compose files is obsolete but kept for readability
* This project is designed for **learning and demonstration purposes**

---

## 👤 Author

DevOps & Cloud Engineer (Junior)

---

## ✅ Status

✔️ Functional
✔️ Authenticated
✔️ Production-like Docker architecture
