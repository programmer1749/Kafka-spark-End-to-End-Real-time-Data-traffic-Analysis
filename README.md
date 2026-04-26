
# Mobility Data Platform

Welcome to the Mobility Data Platform! This project provides a ready-to-use, containerized big data analytics stack for local development, data engineering, and BI reporting. It integrates Apache Hive, Spark, Kafka, and PostgreSQL, and is designed for easy connection to Power BI.

---

## 🚀 Quick Start

1. **Clone this repository**
2. **Start all services:**
   ```sh
   docker-compose up -d
   ```
3. **Initialize Hive Metastore schema:**
   ```sh
   docker exec -it hive-metastore schematool -dbType postgres -initSchema
   ```
4. **Connect Power BI or other BI tools** (see below)

---

## 🏗️ Architecture Overview

```
┌────────────┐      ┌──────────────┐      ┌────────────┐     
│  Power BI  │◀───▶│   Hive       │◀───▶│ PostgreSQL │
└────────────┘      │ Metastore    │      │ (Metastore)│ 
      ▲            └─────┬────────┘       └────────────┘
      │                  │
      │                  ▼
┌────────────┐      ┌────────────┐
│   Spark    │◀───▶│   Kafka    │
└────────────┘      └────────────┘
```

- **Hive Metastore**: Central metadata store for Spark and Hive tables (backed by PostgreSQL)
- **Spark**: Distributed data processing engine
- **Kafka**: Real-time streaming platform
- **Power BI**: Connects via Hive JDBC/ODBC for analytics

---

## ⚙️ Prerequisites

- [Docker](https://www.docker.com/get-started) and [Docker Compose](https://docs.docker.com/compose/)
- Windows, macOS, or Linux
- Power BI Desktop (for BI integration)

---

## 🛠️ Common Operations

### Start All Services
```
docker-compose up -d
```

### Stop All Services
```
docker-compose down
```

### View Logs
```
docker logs <container-name>
```

### Remove All Data (Dangerous!)
```
docker-compose down -v
```

### Initialize Hive Metastore (run once after DB reset)
```
docker exec -it hive-metastore schematool -dbType postgres -initSchema
```

---

## 📊 Power BI Integration

1. **Install the Hive ODBC Driver** (if not already installed)
2. **Get Hive connection details** from your `hive-site.xml` (host, port, database, user, password)
3. **In Power BI Desktop:**
   - Go to `Get Data` → `ODBC` or `Hive` (if available)
   - Enter the connection string and credentials
   - Load your tables for analytics and visualization

**Tip:** If you have trouble connecting, check that the Hive Metastore container is running and the schema is initialized.

---

## 🧑‍💻 Troubleshooting

- **Hive schema initialization fails:**
  - Make sure the PostgreSQL container is running and the database is clean (see logs for details)
  - Remove the Postgres Docker volume if you need a full reset
- **Power BI can't connect:**
  - Double-check the JDBC/ODBC connection details
  - Ensure the Hive Metastore container is running
- **Other issues:**
  - Use `docker logs <container-name>` to view logs
  - Check your `hive-site.xml` and `docker-compose.yml` for correct settings

---

## 📁 Project Structure

- `docker-compose.yml` — Service definitions for the platform
- `hive-conf/hive-site.xml` — Hive and metastore configuration
- `warehouse/` — Data warehouse storage (mounted in containers)
- `apps/` — Example Spark/Hive applications
- `producer/` — Example Kafka producer scripts

---

## 🤝 Contributing & Support

Feel free to open issues or pull requests for improvements. For help, check the logs, review the config files, or ask for support!

---

**Happy Data Engineering!**
