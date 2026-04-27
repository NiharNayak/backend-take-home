# 🎮 ArcadeHub — Backend Engineering Take-home Assignment
> **Intern Interview Challenge · Microservices API**

---

## Overview

You are building the backend for **ArcadeHub**, a gaming portal. Your task is to design and implement a small set of microservices that power the game catalog and leaderboard features.

Focus on **clean API design**, **proper data modeling**, and **sensible separation of concerns** — not on building something massive.

| | |
|---|---|
| ⏱ **Suggested time** | 4–6 hours |
| 🛠 **Stack** | Your choice (Node.js, Python, Go, etc.) |
| 📦 **Style** | REST / Microservices |

---

## Services to Build

### 1. Game Catalog Service
Manages the list of available games on the platform.

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/games` | List all available games (optional filters: `genre`, `status`) |
| `GET` | `/games/:id` | Fetch details of a specific game |
| `POST` | `/games` | Add a new game to the catalog (admin action) |

**Sample game object:**
```json
{
  "id": "uuid",
  "title": "Shadow Runners",
  "genre": "platformer",
  "status": "active",
  "released_at": "2024-03-15"
}
```

---

### 2. Leaderboard Service
Tracks player scores and computes rankings per game.

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/leaderboard/:gameId` | Return top 10 scorers for a given game |
| `GET` | `/leaderboard/global` | Return top 10 scorers across all games |
| `POST` | `/scores` | Submit a new score for a player and game |

**Sample leaderboard response:**
```json
{
  "game_id": "uuid",
  "rankings": [
    { "rank": 1, "player": "shadow_x", "score": 98200 },
    { "rank": 2, "player": "nova99",   "score": 87450 }
  ]
}
```

---

### 3. Player Service *(lightweight)*
Basic player identity — no authentication required, keep it simple.

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/players` | Register a player (username + email) |
| `GET` | `/players/:id/scores` | Get all scores submitted by a player |

---

## Technical Requirements

Each service should run **independently** (separate ports or processes). They may share a database or use separate ones — document your choice and reasoning.

- [ ] RESTful API design with consistent JSON responses
- [ ] Basic input validation with meaningful error messages
- [ ] Proper HTTP status codes (`200`, `201`, `400`, `404`, `409`, etc.)
- [ ] A `README.md` explaining how to run all services locally
- [ ] At least **one set of unit or integration tests** for the leaderboard ranking logic

---

## Bonus *(optional — only if time allows)*

These are not expected but are good to explore if you finish early:

- 🐳 **Docker / docker-compose** setup to run all services together
- ⚡ **Caching** on the leaderboard endpoint (e.g. Redis or a simple in-memory TTL cache)
- 📄 **Pagination** on `/games` and `/players/:id/scores`
- 🔀 **API Gateway** routing all services under a single base URL

---

## What to Submit

Please share a **GitHub repository** (public or private, add us as collaborators) containing:

1. Source code for all three services
2. A `README.md` with clear instructions to run everything locally
3. Sample API requests — either a Postman collection, curl commands, or an `.http` file
4. A short written note (in the README or a separate `DECISIONS.md`) covering:
   - Your database choice and schema design
   - Any trade-offs you made given the time constraint
   - What you would improve or revisit with more time

---

## Evaluation Criteria

| Area | What we look at |
|------|----------------|
| **API design** | Are endpoints intuitive? Are status codes and error messages consistent? |
| **Code quality** | Is the code readable, organized, and easy to follow? |
| **Data modeling** | Does the schema make sense for the problem? |
| **Correctness** | Does the leaderboard return accurate rankings? Are edge cases handled? |
| **Communication** | Does the README work end-to-end? Is the trade-off note thoughtful? |

---

> We value **clarity and reasoning** over complexity. A simple, well-structured solution is preferred over an over-engineered one. Good luck — we look forward to reading your submission! 🚀
