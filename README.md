
# 🚀 Data Ingestion API System

This project implements a RESTful API system to handle data ingestion requests. The system supports batch processing with rate limiting and prioritization of tasks based on their priority level.

---

## 📌 Features

- Submit ingestion jobs with ID arrays and a priority (`HIGH`, `MEDIUM`, `LOW`)
- Process jobs in asynchronous batches of up to 3 IDs
- Enforce a processing rate limit: 1 batch every 5 seconds
- Prioritize high-priority tasks over medium and low
- Simulated external API call (mocked with delay)
- Check the status of each ingestion job and its batches

---

## 🛠 Tech Stack

- **Backend**: Node.js, Express.js
- **Async Processing**: Custom job queue with setInterval
- **Status Tracking**: In-memory store
- **Testing**: Jest, Supertest
- **UUIDs**: For unique batch and ingestion IDs

---

## 📬 API Endpoints

### 1. **POST /ingest**

Submit a new ingestion request.

#### Request

```json
{
  "ids": [1, 2, 3, 4, 5],
  "priority": "HIGH"
}
```

- `ids`: List of integers between 1 and 10^9+7
- `priority`: "HIGH", "MEDIUM", or "LOW"

#### Response

```json
{
  "ingestion_id": "abc123"
}
```

---

### 2. **GET /status/:ingestion_id**

Retrieve the current status of an ingestion request.

#### Example Response

```json
{
  "ingestion_id": "abc123",
  "status": "triggered",
  "batches": [
    {
      "batch_id": "uuid1",
      "ids": [1, 2, 3],
      "status": "completed"
    },
    {
      "batch_id": "uuid2",
      "ids": [4, 5],
      "status": "triggered"
    }
  ]
}
```

#### Status Logic

- Batch-level: `yet_to_start`, `triggered`, `completed`
- Ingestion-level:
  - All batches `yet_to_start` → `yet_to_start`
  - At least one `triggered` → `triggered`
  - All batches `completed` → `completed`

---

## ⚙️ How It Works

1. IDs are split into batches of 3.
2. Each batch is assigned a unique ID and queued.
3. The queue respects priority and creation time.
4. A background processor handles 1 batch every 5 seconds.
5. Each ID is processed with a mocked delay (simulating external API).

---

## 🧪 Running Locally

```bash
git clone https://github.com/aayushmehta01/ingestion
cd ingestion
npm install
node server.js
```

App runs on `http://localhost:5000`

---
