
# DevOps Reverse Proxy with Docker, Nginx, Go, and Python

## 📦 Project Overview

This project sets up a microservices architecture using Docker Compose. It consists of:

- A **Go (Golang)** application (Service 1)
- A **Flask (Python)** application (Service 2)
- An **Nginx reverse proxy** that routes requests to the appropriate service based on the URL path prefix.

All services run in isolated Docker containers and communicate via a custom bridge network.

---

## 🗂️ Project Structure

```
.
├── docker-compose.yml
├── nginx
│   ├── nginx.conf
│   └── Dockerfile
├── service_1
│   ├── main.go
│   └── Dockerfile
├── service_2
│   ├── app.py
│   └── Dockerfile
└── README.md
```

---

## 🚀 How to Run the Project

Make sure you have Docker and Docker Compose installed.

```bash
docker-compose up --build
```

> This will build and run all services. Nginx will be accessible at `http://localhost:8080`.

---

## 🌐 Routing Rules (via Nginx)

- `http://localhost:8080/service1/ping` → routed to Go Service (Service 1)
- `http://localhost:8080/service1/hello` → routed to Go Service (Service 1)
- `http://localhost:8080/service2/ping` → routed to Flask Service (Service 2)
- `http://localhost:8080/service2/hello` → routed to Flask Service (Service 2)

---

## 📄 Nginx Configuration Highlights

- Reverse proxy rules based on path prefixes (`/service1`, `/service2`)
- Logs every incoming request with timestamp and path

Example log format:
```
[$time_local] $remote_addr requested $request_uri
```

---

## ❤️ Bonus Features

- **Health Checks**:
  - Service 1: Responds to `/ping`
  - Service 2: Responds to `/ping`
- **Nginx Logs**: Custom logging added for debugging and monitoring
- **Bridge Network**: Ensures isolated inter-container communication

---

## 🧪 Testing the Setup

Once services are up, visit these URLs:

| URL                                | Description                   |
|------------------------------------|-------------------------------|
| `http://localhost:8080/service1/ping`  | Healthcheck - Go App         |
| `http://localhost:8080/service1/hello` | Hello Message - Go App       |
| `http://localhost:8080/service2/ping`  | Healthcheck - Flask App      |
| `http://localhost:8080/service2/hello` | Hello Message - Flask App    |

---

## 📝 Notes

- Uses `curl` for health checks in the Docker Compose file.
- Make sure port `8080` is not used by other services on your machine.

---

---

## 👤 Author

*Name:* Prashanth Bonkuru 
---

## 🛠️ Tools Used

- Docker & Docker Compose
- Go (net/http)
- Flask (Python)
- Nginx
