Here's a **detailed data model** for the **AI Fitness Coach (ALIVE Coach)** product, aligned with your PRD. This includes key **entities**, their **attributes**, and **relationships** across user profile, health metrics, fitness planning, AI interaction, and behavioral feedback.

---

# **Data Model: AI Fitness Coach (ALIVE Coach)**

## **1. Entity Relationship Diagram (ERD) - Overview**

### Core Entities:

* `User`
* `DailyLog`
* `WorkoutPlan`
* `WorkoutSession`
* `HealthMetric`
* `MenstrualCycle`
* `HabitTracker`
* `AIInteraction`
* `Goal`
* `Recommendation`

Relationships:

* A `User` has many `DailyLogs`, `WorkoutPlans`, `HealthMetrics`, `HabitTrackers`, `Goals`, and `AIInteractions`.
* Each `WorkoutPlan` consists of many `WorkoutSessions`.
* `AIInteraction` generates `Recommendation`s tied to the user’s state.

---

## **2. Detailed Table Definitions**

### **2.1. User**

| Field              | Type      | Description                    |
| ------------------ | --------- | ------------------------------ |
| user\_id           | UUID (PK) | Unique user identifier         |
| name               | STRING    | User name                      |
| email              | STRING    | Login credential               |
| age                | INT       | User’s age                     |
| gender             | STRING    | Male, Female, Non-binary, etc. |
| height\_cm         | FLOAT     | User height in cm              |
| weight\_kg         | FLOAT     | Starting weight                |
| target\_weight\_kg | FLOAT     | Goal weight                    |
| timezone           | STRING    | For time-based coaching        |
| created\_at        | TIMESTAMP | Registration time              |

---

### **2.2. DailyLog**

| Field                 | Type      | Description                        |
| --------------------- | --------- | ---------------------------------- |
| log\_id               | UUID (PK) | Daily log entry ID                 |
| user\_id              | UUID (FK) | Reference to User                  |
| date                  | DATE      | Daily record date                  |
| energy\_level         | INT       | Self-reported (1–5)                |
| mood                  | STRING    | Happy, Tired, Anxious, etc.        |
| sleep\_hours          | FLOAT     | Total hours slept                  |
| water\_intake\_liters | FLOAT     | Water intake                       |
| digestion\_score      | INT       | 1–5 (e.g., ease of bowel movement) |
| cycle\_phase          | STRING    | (optional) Menstrual phase         |
| ai\_notes             | TEXT      | AI-generated summary               |

---

### **2.3. HealthMetric**

| Field      | Type      | Description                                  |
| ---------- | --------- | -------------------------------------------- |
| metric\_id | UUID (PK) | Health record ID                             |
| user\_id   | UUID (FK) | Reference to User                            |
| timestamp  | TIMESTAMP | Time of reading                              |
| type       | STRING    | e.g., HRV, Resting HR, Steps, Weight         |
| value      | FLOAT     | Metric value                                 |
| source     | STRING    | Device/App (Apple Watch, Manual, Oura, etc.) |

---

### **2.4. MenstrualCycle**

| Field                | Type      | Description                               |
| -------------------- | --------- | ----------------------------------------- |
| cycle\_id            | UUID (PK) | Record ID                                 |
| user\_id             | UUID (FK) | Reference to User                         |
| start\_date          | DATE      | Start of period                           |
| end\_date            | DATE      | End of period                             |
| predicted\_ovulation | DATE      | (Optional)                                |
| symptoms             | JSON      | { "cramps": true, "mood\_swings": false } |

---

### **2.5. WorkoutPlan**

| Field                | Type      | Description                              |
| -------------------- | --------- | ---------------------------------------- |
| plan\_id             | UUID (PK) | Workout Plan ID                          |
| user\_id             | UUID (FK) | Reference to User                        |
| plan\_start\_date    | DATE      | Start of workout plan                    |
| plan\_type           | STRING    | e.g., Weight Loss, Strength, Flexibility |
| goal\_id             | UUID (FK) | Reference to user’s Goal                 |
| frequency\_per\_week | INT       | e.g., 5 workouts/week                    |
| ai\_generated        | BOOLEAN   | True if created by AI                    |

---

### **2.6. WorkoutSession**

| Field             | Type      | Description                |
| ----------------- | --------- | -------------------------- |
| session\_id       | UUID (PK) | Session ID                 |
| plan\_id          | UUID (FK) | Reference to WorkoutPlan   |
| date              | DATE      | Planned date               |
| duration\_minutes | INT       | Planned or actual duration |
| activity\_type    | STRING    | e.g., HIIT, Yoga, Strength |
| intensity\_level  | STRING    | Light, Moderate, Intense   |
| calories\_burned  | FLOAT     | Estimated or real          |
| completed         | BOOLEAN   | True if finished           |

---

### **2.7. HabitTracker**

| Field       | Type      | Description                            |
| ----------- | --------- | -------------------------------------- |
| habit\_id   | UUID (PK) | Habit entry                            |
| user\_id    | UUID (FK) | Reference to User                      |
| date        | DATE      | When habit was logged                  |
| habit\_type | STRING    | e.g., Water, Meditation, Sleep by 11PM |
| status      | BOOLEAN   | Completed or not                       |
| notes       | TEXT      | Optional reflection                    |

---

### **2.8. AIInteraction**

| Field            | Type      | Description                                    |
| ---------------- | --------- | ---------------------------------------------- |
| interaction\_id  | UUID (PK) | Interaction ID                                 |
| user\_id         | UUID (FK) | Reference to User                              |
| timestamp        | TIMESTAMP | When conversation happened                     |
| input\_text      | TEXT      | User message                                   |
| response\_text   | TEXT      | AI’s reply                                     |
| action\_type     | STRING    | e.g., motivation, workout change, mood support |
| session\_context | JSON      | Summary of state at time of interaction        |

---

### **2.9. Recommendation**

| Field              | Type      | Description                                                         |
| ------------------ | --------- | ------------------------------------------------------------------- |
| recommendation\_id | UUID (PK) | ID                                                                  |
| user\_id           | UUID (FK) | Reference to User                                                   |
| timestamp          | TIMESTAMP | When given                                                          |
| category           | STRING    | Workout, Sleep, Nutrition, Mindset                                  |
| content            | TEXT      | Specific suggestion or advice                                       |
| based\_on          | JSON      | Inputs like { "sleep": 4, "cycle\_phase": "luteal", "mood": "low" } |

---

### **2.10. Goal**

| Field           | Type      | Description                     |
| --------------- | --------- | ------------------------------- |
| goal\_id        | UUID (PK) | ID                              |
| user\_id        | UUID (FK) | Reference to User               |
| goal\_type      | STRING    | e.g., Lose 10kg, Sleep 8h/night |
| target\_value   | FLOAT     | e.g., 60.0kg                    |
| progress\_value | FLOAT     | Latest progress                 |
| target\_date    | DATE      | Intended achievement date       |
| status          | STRING    | Active, Paused, Completed       |

---

## **3. Notes on Architecture**

### Integrations

* Apple Health, Fitbit, Garmin APIs feed `HealthMetric`
* Period tracking APIs feed `MenstrualCycle`
* LLM-based NLP feeds `AIInteraction` and `Recommendation`

### AI Layer Logic (On top of data model)

* Daily planner reads: `DailyLog`, `HealthMetric`, `Cycle`, `Goal`
* Generates: `WorkoutSession`, `HabitTracker`, `Recommendation`
* Learns and adjusts over time via Reinforcement Learning feedback loop

---


