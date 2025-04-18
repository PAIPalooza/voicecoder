---

# 📘 Product Requirements Document (PRD)

## 🧭 Overview
**Voice-Coded ToDo List** is an AI-powered productivity app that allows users to add, timestamp, and manage tasks using natural voice commands. By leveraging the **Hume API** for voice transcription and emotional intelligence, the app understands user intent and prioritizes tasks accordingly.

## 🚀 Goals
- Enable users to **add tasks via voice** with automatic transcription.
- **Timestamp** each task based on voice input and metadata.
- Use **emotional tone (via Hume)** to set task urgency or sentiment context.
- Sync tasks across sessions/devices.
- Simple and clean UI/UX optimized for mobile and voice-first interaction.

## 🧩 Core Features

| Feature                          | Description |
|----------------------------------|-------------|
| 🎤 Voice Command Input           | Users speak to the app to create tasks. |
| 🧠 Hume API Integration          | Extract transcription, intent, and emotional context. |
| 🕒 Timestamping                  | Tasks are automatically timestamped on creation. |
| ⚡ Sentiment-Based Prioritization| Emotions like urgency or stress flag higher-priority tasks. |
| 📝 Task Editing & Deletion       | Update or remove tasks with follow-up voice or text commands. |
| ☁️ Cloud Sync (Optional)        | Sync across devices using Supabase or Firebase. |
| 📱 UI for Task List              | Mobile-first interface showing tasks by priority and time. |

---

## 🛠️ Technical Architecture

### 🎤 Input Pipeline
1. **Microphone Input** (native browser/mobile API)
2. Stream audio to **Hume API**
3. Receive structured response: 
   ```json
   {
     "transcription": "Buy groceries",
     "timestamp": "2025-04-18T10:00:00Z",
     "emotions": {
       "urgency": 0.85,
       "stress": 0.65
     }
   }
   ```

### 🧠 Backend
- **FastAPI** for RESTful services
- **Supabase** or **Firebase** for auth & task storage
- Store:
  - `task_text`
  - `created_at`
  - `emotional_score`
  - `priority_flag`

### 🖼️ Frontend
- Built with **Next.js** or **React Native** (depending on mobile/web target)
- Voice input button
- Task list UI
- Priority tags/icons from emotion scores

---

## 🗃️ Data Model (Supabase or PostgreSQL)

```sql
Table: tasks
- id (UUID, Primary Key)
- user_id (UUID, Foreign Key)
- task_text (Text)
- created_at (Timestamp)
- emotion_data (JSONB)
- priority_flag (Boolean)
```

---

## ✅ User Stories

### Epic: Voice-to-Task Flow

| ID | As a user, I want to...                                      | Acceptance Criteria |
|----|--------------------------------------------------------------|----------------------|
| T1 | Add a task using voice                                       | Task appears in list with correct text & timestamp |
| T2 | See tasks ordered by urgency/emotion                        | High-emotion tasks appear at top |
| T3 | Edit or delete a task via voice                             | Task updates or disappears from UI |
| T4 | See real-time feedback of my command                        | Live transcription shown as I speak |
| T5 | Use app without needing to touch keyboard                   | 100% voice-only flow supported |

---

## 🧪 Testing Strategy

- **Unit tests** for API endpoints and task logic
- **E2E tests** for voice-to-task workflow using mock Hume responses
- **Mock fallback mode** for offline voice testing
- **BDD-style tests** for user flows using `pytest-bdd` or Cypress

---

## 📅 Sprint Breakdown (1-Day Hackathon MVP)

### Sprint Goal: Build a working prototype for voice-to-task creation

| Task | Description | Est. Hours |
|------|-------------|------------|
| Setup FastAPI Backend | Auth, DB, endpoints | 2h |
| Integrate Hume API | Voice input, parse emotion | 2h |
| Build UI | React or React Native voice-enabled interface | 2h |
| Task List Component | Display sorted tasks | 1h |
| Test & Deploy | QA and deploy to Vercel or Render | 1h |

---

## 🔗 Hume API Setup Notes
- Use `/v0/stream` for real-time voice input
- Parse `emotions` for urgency/stress
- Map scores > 0.75 to high-priority

---
