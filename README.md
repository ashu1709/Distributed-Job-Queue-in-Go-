# ⚙️ Distributed Job Queue in Go

A robust, distributed background task queue built in **Go**, designed for scalability, concurrency, and reliability.  
It handles asynchronous job execution across different services, with support for various job types and scheduling strategies.

---

## 🔑 Key Features

- 🚀 High-performance concurrent processing using Go routines  
- 🧠 Topic-aware job handlers for emails, image processing, and data tasks  
- 🧾 Job queue powered by Redis for fast and persistent task management  
- 📆 Built-in scheduler for recurring jobs using cron-like syntax  
- 🧪 RESTful API to enqueue new jobs from external services  
- ⚙️ Configurable worker pool size and timeout via environment or config file  
- 📉 Intelligent polling with exponential backoff strategy  
- 🗃️ Job result persistence using PostgreSQL  
- 🧩 Modular structure: workers, handlers, scheduler, storage, queue, and config components

---

## 🧱 System Components

### 🔧 Worker (`worker.go`)
- Pulls jobs from Redis queue and processes them concurrently  
- Uses custom handlers based on job type  
- Implements exponential backoff for efficient polling

### 🕒 Scheduler (`scheduler.go`)
- Supports recurring tasks using cron-style expressions

### 📦 Queue (`queue.go`)
- Manages job enqueue/dequeue and status updates in Redis

### 🧾 Job Definitions (`job.go`)
- Structures supported jobs: email, image processing, data pipelines

### 🧠 Handlers (`handler.go`)
- Implements logic for processing each type of job

### 🗃️ Storage (`storage.go`)
- Persists job results using PostgreSQL

### ⚙️ Configuration (`config.go`)
- Managed via Viper, supports `.env` and config-based overrides

---

## 🚀 Getting Started

1. Make sure **Redis** and **PostgreSQL** are running.
2. Configure the environment variables or `config.go` settings.
3. Start the application:
   ```bash
   go run main.go
   ```

---

## 🌐 API Example

Submit a job via HTTP:

**Endpoint:** `POST /submit`  
**Headers:** `Content-Type: application/json`  
**Body:**
```json
{
  "type": "email",
  "payload": {
    "to": "user@example.com",
    "subject": "Hello",
    "body": "This is a sample email."
  }
}
```

---

## ⚙️ Configuration via Environment Variables

| Variable         | Purpose                            | Default              |
|------------------|------------------------------------|----------------------|
| `REDISADDR`      | Redis server address               | `127.0.0.1:6379`     |
| `MAXRETRIES`     | Max retry attempts for a job       | `5`                  |
| `WORKERCOUNT`    | Number of concurrent workers       | `10`                 |
| `APIADDR`        | API server bind address            | `127.0.0.1:8080`     |
| `WORKERTIMEOUT`  | Time in seconds before worker exits| `10`                 |

---

## 🔌 Extending the System

To add a new job type:
1. Define the new job schema in `job.go`  
2. Implement its handler logic in `handler.go`  
3. Register the new handler in `main.go`

---

## 🤝 Contributing

Contributions are welcome! Feel free to fork, build on, or submit pull requests.

---

## 📄 License

This project is licensed under the MIT License.
