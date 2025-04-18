
---

# 🏃 Agile Sprint Plan – *Voice-Coded ToDo List*

### 🗓️ Sprint Duration:
- **Standard Version**: 5–7 days
- **Hackathon Version**: 8-hour compressed day (noted with ⏱️)

---

## 🧭 Sprint Goal
Build a production-ready MVP that:
- Accepts voice input
- Transcribes tasks using Hume API
- Stores tasks with emotion-based metadata and timestamps
- Displays a prioritized to-do list based on emotional urgency

---

## 🎯 Sprint Themes / Epics

| Epic ID | Epic Title                     | Description |
|---------|--------------------------------|-------------|
| E1      | Voice Command Capture          | Handle voice input and stream to Hume |
| E2      | Emotion + Transcription Parsing| Handle Hume API response and extract key data |
| E3      | Task Management Backend        | API and DB setup for task CRUD |
| E4      | Prioritized Task Display       | Display sorted list with UX elements |
| E5      | TDD/BDD Testing Infrastructure | Ensure robust, test-first coverage |
| E6      | Deployment + DevOps            | Ship to Vercel or Render, env setup |

---

## 📋 Backlog Breakdown (Stories + SSCS Scoring)

| Story ID | User Story | Epic | Score (Fibonacci) | Type | Notes |
|----------|------------|------|-------------------|------|-------|
| S1 | As a user, I want to press a button and speak my task | E1 | 2 | Feature | Basic mic input |
| S2 | As a developer, I want to stream the voice to the Hume API | E1 | 3 | Tech Spike | Ensure live stream support |
| S3 | As the system, I want to receive transcription and emotional metadata from Hume | E2 | 2 | Feature | Map `urgency`, `stress` |
| S4 | As a developer, I want to convert emotion data to a `priority_flag` | E2 | 1 | Logic | Score > 0.75 = priority |
| S5 | As a user, I want my tasks to be timestamped automatically | E3 | 1 | Feature | `created_at` auto field |
| S6 | As a user, I want to see my tasks displayed in order of priority and time | E4 | 2 | Feature | Sort by priority → time |
| S7 | As a developer, I want a FastAPI backend with `/tasks` endpoints | E3 | 3 | Infra | GET/POST with TDD |
| S8 | As a dev, I want Supabase or SQLite setup for task persistence | E3 | 2 | Infra | Choose based on dev speed |
| S9 | As a user, I want to delete a task | E3 | 1 | Feature | Basic delete |
| S10 | As a user, I want visual confirmation when a task is added | E4 | 1 | UX | Toast/snackbar |
| S11 | As a dev, I want unit tests for all backend logic | E5 | 2 | QA | Use `pytest` or `unittest` |
| S12 | As a dev, I want E2E tests for voice-to-task flow | E5 | 3 | QA | Mock Hume API |
| S13 | As a dev, I want to deploy the app for demo | E6 | 2 | DevOps | Vercel or Render |
| S14 | As a dev, I want to load test task creation | E6 | 1 | QA | Optional for MVP |

---

## 🧪 TDD/BDD Test Matrix

| Feature | Test Type | Description |
|---------|-----------|-------------|
| Voice Input | Unit | Mic API triggers recording |
| Hume API | Integration | Response includes text + emotion |
| Task Creation | Unit + E2E | Creates valid record in DB |
| Priority Logic | Unit | Flags if urgency > 0.75 |
| Task Display | E2E | Sorted by priority then time |
| Delete Task | Unit | Removes correct record |
| UI Feedback | E2E | Visual confirmation shown |
| API Routes | Unit | `/tasks` POST, GET, DELETE coverage |

---

## 🧱 Task Allocation by Role

| Role | Responsibilities |
|------|------------------|
| 🧑‍💻 Frontend Dev | S1, S6, S10 |
| 🧑‍🔧 Backend Dev | S3, S4, S5, S7, S8, S9 |
| 🧪 QA/Test Engineer | S11, S12, S14 |
| 🧑‍🎨 UI/UX | Task list, priority color indicators |
| 🚀 DevOps | S13 |

---

## 📦 Deliverables (End of Sprint)

- 🎤 Voice recording button
- 🔊 Transcription + emotion parsing via Hume
- 📦 FastAPI backend with task CRUD
- 📋 Prioritized task list UI
- 🧪 Unit and E2E tests
- ☁️ Deployment link for demo

---
