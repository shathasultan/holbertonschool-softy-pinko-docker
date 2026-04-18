# holbertonschool-softy-pinko-docker

Docker-based infrastructure project for **Softy Pinko** with progressive tasks:

- Task 0: First Ubuntu image
- Task 1: Flask back-end API (`/api/hello`)
- Task 2: Nginx front-end static hosting
- Task 3: Front-end ↔ back-end integration with CORS
- Task 4: Multi-service orchestration with Docker Compose
- Task 5: Reverse proxy with Nginx
- Task 6: Horizontal scaling for API servers

## Prerequisites

- Docker Desktop (or Docker Engine + Compose)
- Git

## Project Structure

- `task0/` Basic Docker image
- `task1/` Flask API container
- `task2/` Back-end + front-end images
- `task3/` Dynamic front-end data from API
- `task4/` `docker-compose.yml` for front/back services
- `task5/` Proxy service + compose routing
- `task6/` Scaled API setup + `2-api-servers.txt`
- `inst` Original project instructions

## Quick Start

### Task 0

```bash
cd task0
docker build -t softy-pinko:task0 .
docker run --rm softy-pinko:task0
```

### Task 1

```bash
cd task1
docker build -t softy-pinko:task1 .
docker run --rm -p 5252:5252 softy-pinko:task1
```

Then open:

- http://localhost:5252/api/hello

### Task 2 (front-end)

```bash
cd task2
docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
docker run --rm -p 9000:9000 softy-pinko-front-end:task2
```

Then open:

- http://localhost:9000

### Task 4 (compose example)

```bash
cd task4
docker compose build
docker compose up
```

### Task 5 (proxy entrypoint)

```bash
cd task5
docker compose build
docker compose up
```

Then open:

- http://localhost

### Task 6 (scale API servers)

```bash
cd task6
docker compose up --scale back-end=2
```

(Exact command is also stored in `task6/2-api-servers.txt`.)

## Notes

- Back-end service listens on port `5252`.
- Front-end Nginx service listens on port `9000`.
- Proxy service listens on port `80` and routes:
  - `/` → front-end
  - `/api` → back-end
- Round-robin load balancing is provided by Nginx when `back-end` is scaled with Docker Compose.

## Author

Prepared for Holberton Docker project practice.
