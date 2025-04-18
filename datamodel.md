---

# 📊 Data Model: Voice-Coded ToDo List

## 🎯 Core Entities
There are 2 primary entities:
1. `users` – for user authentication and session linkage (via Supabase Auth or custom JWT)
2. `tasks` – the main object capturing the voice-coded tasks

---

## 🧑 Table: `users`

| Field Name     | Type         | Constraints                 | Description                            |
|----------------|--------------|-----------------------------|----------------------------------------|
| `id`           | UUID         | PK, Required                | Unique user ID                         |
| `email`        | Text         | Unique, Indexed             | User email (login identifier)          |
| `created_at`   | Timestamp    | Default: now()              | Account creation timestamp             |
| `auth_provider`| Text         | Optional                    | e.g., 'supabase', 'google', 'github'   |
| `last_login`   | Timestamp    | Optional                    | Last login time                        |

---

## ✅ Table: `tasks`

| Field Name     | Type         | Constraints                 | Description                            |
|----------------|--------------|-----------------------------|----------------------------------------|
| `id`           | UUID         | PK, Required                | Unique task ID                         |
| `user_id`      | UUID         | FK → users.id, Required     | Associated user                        |
| `task_text`    | Text         | Not Null                    | Transcribed text from voice            |
| `created_at`   | Timestamp    | Default: now()              | When the task was added                |
| `emotion_data` | JSONB        | Optional                    | Full emotion breakdown from Hume       |
| `priority_flag`| Boolean      | Default: false              | True if emotional score > 0.75         |
| `source_audio_url` | Text    | Optional                    | URL for stored audio (if persisted)    |
| `is_completed` | Boolean      | Default: false              | Completion status                      |
| `deleted_at`   | Timestamp    | Optional                    | For soft deletion                      |

---

## 🧠 Emotion Metadata Schema (inside `emotion_data` JSONB)

Hume returns emotional insights. We store this as raw JSON for flexibility.

Example:

```json
{
  "emotion_scores": {
    "urgency": 0.87,
    "stress": 0.75,
    "satisfaction": 0.20
  },
  "dominant_emotion": "urgency"
}
```

---

## 🗂️ Optional Table: `task_logs` *(for audit/history)*

| Field Name   | Type       | Description |
|--------------|------------|-------------|
| `id`         | UUID       | PK |
| `task_id`    | UUID       | FK → tasks.id |
| `event`      | Text       | 'created', 'updated', 'deleted' |
| `old_data`   | JSONB      | Snapshot before change |
| `new_data`   | JSONB      | Snapshot after change |
| `timestamp`  | Timestamp  | Event timestamp |

---

## 🔐 Supabase Auth Integration (User Linking)
If using Supabase:
- `user_id` in `tasks` will map to `auth.users.id`
- Use RLS (Row Level Security) policies to ensure users can only access their own tasks

---

## 🧪 Example Record

```json
{
  "id": "b12a5670-3045-11ee-be56-0242ac120002",
  "user_id": "1c213f64-89ae-4c42-b9e1-42a3cb3441f9",
  "task_text": "Buy oat milk and eggs",
  "created_at": "2025-04-18T10:31:00Z",
  "emotion_data": {
    "emotion_scores": {
      "urgency": 0.88,
      "stress": 0.81
    },
    "dominant_emotion": "urgency"
  },
  "priority_flag": true,
  "is_completed": false
}
```

---
