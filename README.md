# Quiz Leaderboard System (Java) — Validator Integration

This is a real-world style **Spring Boot web application** that:

- Polls the validator **10 times** (`poll=0..9`) with a **mandatory 5 second delay** between polls
- Deduplicates events by **(roundId + participant)**
- Aggregates scores per participant
- Generates a leaderboard sorted by `totalScore` (descending)
- Computes total score across all users
- Submits the leaderboard **exactly once** and persists that submission state locally

## Prerequisites

- Java 17 installed (`java -version` should work)

No Maven installation needed (this repo uses **Maven Wrapper**).

## Configure

Set your registration number (recommended as env var):

PowerShell:

```powershell
$env:QUIZ_REG_NO="2024CS101"
```

## Run

```powershell
cd "c:\Users\91707\OneDrive\Desktop\bajaj"
.\mvnw.cmd spring-boot:run
```

Open the UI:

- `http://localhost:8080/`

## API

- `POST /api/run`: starts the run in background
- `GET /api/status?jobId=...`: check status and fetch result when done
- `GET /api/last`: returns last persisted state (including whether submission already happened)

## “Submit only once” behavior

After a successful submit, a local file is written to:

- `data/run-state.json`

If you click **Run** again with the same `QUIZ_REG_NO`, the app will **not submit again** and will return the persisted result instead.

