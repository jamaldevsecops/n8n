# n8n Docker Setup (with PostgreSQL + RabbitMQ + Queue Workers)

This repository contains a production-ready deployment of [n8n](https://n8n.io) using Docker Compose, with:

- PostgreSQL for workflow and credential storage
- RabbitMQ for queue mode execution
- Separate `worker` container for scalable processing
- Bind mounts for persistent storage
- Health checks
- Environment variables via `.env`

---

## 🗂 Directory Structure

```
n8n/
├── docker-compose.yaml   # Main deployment file
├── .env                  # Environment variables (secrets)
├── n8n_data/             # Mounted config directory for n8n
├── postgres_data/        # Mounted storage for PostgreSQL
```

---

## 🚀 How to Run

1. Clone the repo:

```bash
git clone https://github.com/jamaldevsecops/n8n.git
cd n8n
```

2. Create directories for persisting the data

```bash
mkdir n8n_data postgres_data
```

3. Start the services:

```bash
docker-compose pull && docker-compose up -d
```

4. Access n8n at: [http://localhost:5678](http://localhost:5678)

5. Access RabbitMQ management UI: [http://localhost:15672](http://localhost:15672)

---

## 🛠 Services

| Service     | Port    | Description                         |
|-------------|---------|-------------------------------------|
| n8n         | 5678    | Main web UI                         |
| PostgreSQL  | 5432    | Database                            |
| RabbitMQ    | 5672    | Queue transport                     |
| RabbitMQ UI | 15672   | Management dashboard (guest/guest)  |

---

## 🧪 Test Queue Mode

To confirm queue mode is working:
- Trigger a workflow that uses delays or long tasks
- Check logs with:

```bash
docker logs -f n8n_worker
```

---

## 📦 Persistent Volumes

- `./n8n_data` → `/home/node/.n8n`
- `./postgres_data` → `/var/lib/postgresql/data`

---

## 🔐 Security Tips

- Use HTTPS via reverse proxy (e.g., Nginx)
- Set `N8N_HOST` to your public domain
- Rotate credentials regularly

---

## 🧹 Cleanup

To stop and remove all services:

```bash
docker-compose down
```

To also remove volumes:

```bash
docker-compose down -v
```

---

## 📜 License

MIT — Use freely, but use wisely!