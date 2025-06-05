# 🚀 Data Ingestion API System

This project implements a simple RESTful API system to ingest and track the processing of data IDs. It simulates external API calls, processes IDs in batches, enforces a rate limit, and respects priority-based ordering.

---

## 📌 Features

- Submit ingestion jobs with priority (`HIGH`, `MEDIUM`, `LOW`)
- Asynchronous batch processing (3 IDs per batch)
- Priority queue: HIGH > MEDIUM > LOW
- Rate limit: 1 batch per 5 seconds
- Track ingestion and batch processing status
- Mocked external API with simulated delay

---

## 🛠 Tech Stack

- Node.js
- Express.js
- UUID for batch/job IDs
- In-memory store for status tracking
- Jest & Supertest for testing

---

## 📬 API Endpoints

### 1. **POST /ingest**

Submit a list of IDs for processing.

**Request Body:**

```json
{
  "ids": [1, 2, 3, 4, 5],
  "priority": "HIGH"
}
```

**Response Body:**

```json
{
  "ingestion_id": "abc123"
}
```

### 2. **GET /status/**

Check status of an ingestion request.

**Response Body:**

```json
{
  "ingestion_id": "abc123",
  "status": "triggered",
  "batches": [
    {
      "batch_id": "uuid-1",
      "ids": [1, 2, 3],
      "status": "completed"
    },
    {
      "batch_id": "uuid-2",
      "ids": [4, 5],
      "status": "triggered"
    }
  ]
}
```

