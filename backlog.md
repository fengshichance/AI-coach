# backlog.md  
**Project**: ALIVE Coach – AI Fitness & Lifestyle Agent  
**Sprint Duration**: 1 Hour  
**Focus**: Core foundation – First pass of backend data schema + prompt engine baseline  
**Sprint Owner**: [Your Name]  
**Date**: 2025-05-13

---

## 🧭 Sprint Goal
Set up the **initial backend structure** and **AI interaction prompt logic** to serve one user end-to-end for Day 1.

---

## ✅ Sprint Deliverables
1. `schema.sql` – Foundational PostgreSQL schema
2. `prompts.md` – Smart coaching prompts (first version)
3. `sample_user_data.sql` – Insert for 1 mock user (Day 1 scenario)
4. `README.md` – Setup and next sprint plan

---

## 🧱 Task Breakdown

### 1. **Data Schema Setup**  
⏱ **Time**: 20 min  
Create schema definitions for core MVP tables:
- `users`
- `daily_logs`
- `workout_sessions`
- `health_metrics`
- `ai_interactions`

**Output**: `schema.sql`

---

### 2. **Smart Prompt Design**  
⏱ **Time**: 20 min  
Write first draft of 3 AI interaction prompts:

| Scenario | Prompt Goal |
|----------|-------------|
| Day 1 Welcome | Set rhythm and build emotional trust |
| Post-sleep Low Energy | Adjust plan and motivate |
| Workout Feedback | Reflect, encourage habit loop |

**Output**: `prompts.md`

---

### 3. **Mock Data Insert**  
⏱ **Time**: 10 min  
Insert test user data for one user:
- Profile: 32F, 169cm, 72kg, goal = 59kg  
- Cycle phase = luteal, mood = low, sleep = 5.5h  
- Workout plan = 30-min yoga  
- Expected AI response: suggest a light stretch + warm nudge

**Output**: `sample_user_data.sql`

---

### 4. **Wrap & Review**  
⏱ **Time**: 10 min  
- Write `README.md`: what's done, what’s next
- Take 1 screenshot or export schema to image
- Optional: Send to ChatGPT or teammate for feedback

**Output**: `README.md`

---

## ✨ Bonus if time permits
- Set up a SQLite local DB and test inserts
- Run mock prompt with GPT (e.g., “User just woke up, didn’t sleep well. What should I say?”)

---

## ⏭️ Next Sprint Ideas
- Connect schema to lightweight Python API
- Build `/coach` endpoint to simulate prompt & response
- Create simple frontend (chat + dashboard mock)
- Add menstrual/cycle sync module

---

## ⛳ Success Criteria
- Can simulate one full Day 1 interaction  
- Data structure supports fitness + emotional + biometric context  
- Prompt system matches user rhythm and offers clear next step

---

