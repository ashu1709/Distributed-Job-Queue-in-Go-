Distributed Job Queue in Go
A scalable and resilient distributed task queue system built in Go, designed for high-performance background job execution and reliable task management across services.

🔧 Key Features
Parallel Job Processing — Efficient use of goroutines for handling multiple jobs concurrently

Redis-backed Queue — Fast and reliable job queuing mechanism using Redis

Recurring Task Scheduling — Supports cron-style recurring jobs

RESTful Job API — Easily submit tasks through an HTTP interface

Configurable Execution — Tune worker count, timeout duration, and queue behavior

Exponential Backoff — Optimized retry and polling strategy for reduced load

Multiple Job Types Supported — Out-of-the-box support for:

Email notifications

Image processing

Custom data jobs

Persistent Job Result Storage — Uses PostgreSQL to log and retrieve job outcomes

🧱 Core Components
🧑‍🔧 Worker (worker.go)
Handles job execution:

Executes tasks in parallel

Dynamically dispatches to appropriate handlers

Implements exponential backoff logic for polling

📅 Scheduler (scheduler.go)
Schedules recurring tasks using cron-like expressions.

🗃️ Queue (queue.go)
Implements Redis-based job operations:

Enqueue

Dequeue

Status tracking

🧾 Job Definition (job.go)
Defines structured formats for various jobs:

Email

Image resizing

Data transformations

🔧 Handlers (handler.go)
Contains logic to process each job type:

Email sending

Image manipulation

Data crunching

🛢️ Storage (storage.go)
Handles job result persistence using PostgreSQL.

⚙️ Configuration (config.go)
Uses Viper to manage:

Redis connection settings

Worker pool size

API server configuration

Timeout durations

🚀 Getting Started
Ensure Redis and PostgreSQL are installed and running.

Configure parameters in config.go or set environment variables.

Run the main Go application.

Submit jobs through a POST request to the /submit endpoint.

🧪 API Usage Example
Endpoint: POST /submit
Headers: Content-Type: application/json

Payload:

json
Copy
Edit
{
  "type": "email",
  "payload": {
    "to": "user@example.com",
    "subject": "Test Email",
    "body": "This is a test email."
  }
}
⚙️ Environment Configuration
You can override defaults using environment variables:

Variable	Description	Default
REDISADDR	Redis server address	127.0.0.1:6379
MAXRETRIES	Max number of job retries	5
WORKERCOUNT	Number of parallel workers	10
APIADDR	API server bind address	127.0.0.1:8080
WORKERTIMEOUT	Worker timeout in seconds	10

➕ Adding New Job Types
Define the job schema in job.go

Implement its logic in handler.go

Register it within main.go

🤝 Contributions
Open to contributions! Please fork the repo and create a pull request.