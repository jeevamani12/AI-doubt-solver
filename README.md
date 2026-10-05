# AI DOUBT SOLVER
> **“Don’t just get the answer. Understand why.”**  
> *A Generative AI Community Hackathon Project powered by Google Gemini.*

---

## 🌟 1. Project Objective & Core Differentiator

Most AI chatbots act as **answer vending machines**—giving immediate answers that encourage passive copying without conceptual understanding. 

**AI Doubt Solver** is an intelligent multimodal Generative AI academic tutor built to solve doubts by understanding **why** a student is struggling. Rather than a generic chat window, it transforms academic questions into a structured pedagogical workflow:

```
Student Doubt (Text, Image, PDF, Voice)
  ↓
Google Gemini Understanding & Multimodal Vision
  ↓
Topic, Subtopic & Question Type Detection
  ↓
Cognitive Misconception Analysis (Trap vs. Mental Model)
  ↓
Personalized Explanation (Adapted to Level & Granularity)
  ↓
Concrete Analogy, Step-by-Step Logic & Runnable Code/Math
  ↓
Exam Marking Mode (2, 5, 10, 15 Marks Structure)
  ↓
Targeted AI Practice Generation
  ↓
Socratic Evaluation & Adaptive Learning Recommendation
```

---

## 🛠️ 2. Technology Stack

- **Frontend:** Next.js 14 App Router, React 18, TypeScript, Tailwind CSS, Lucide React, Framer Motion, Recharts
- **Backend:** Next.js Server Actions, Route Handlers, TypeScript
- **AI Engine:** Google Gemini Generative AI (`gemini-3.5-flash`, `gemini-3.6-flash`, `gemini-3.7-flash`, `gemini-flash-latest`, `gemini-3.8-flash`)
- **Multimodal:** Gemini Vision for handwritten math, textbook diagrams, and screenshots
- **Database:** Supabase PostgreSQL with `pgvector` for semantic search
- **Auth & Storage:** Supabase Auth & Supabase Storage for attachments
- **Local Resilience:** Offline-ready memory/localStorage adapter ensuring zero crashes during evaluation

---

## 🚀 3. Application Pages & Navigation

1. **Landing Page (`/`):** Professional EdTech showcase highlighting the AI Processing Pipeline, multimodal features, and 5 live demo scenarios.
2. **Student Dashboard (`/dashboard`):** Total doubts counter, solved count, practice metrics, learning streak, strong vs. weak topic diagnostic, and Gemini learning sequences.
3. **Ask Doubt (`/ask-doubt`):** Primary multimodal workspace supporting text, image upload, documents, and voice input with academic level, subject, difficulty, explanation style, and exam marks controls.
4. **Teach Me (`/teach-me`):** Socratic 1-on-1 tutoring mode where Gemini introduces concepts, tests student intuition with check questions, and adapts lesson pacing dynamically.
5. **Practice Mode (`/practice`):** Adaptive question generator and Socratic grader scoring student answers (0-100), pinpointing misconceptions, and suggesting next difficulty levels.
6. **Study Material (`/study-material`):** Document intelligence module that strictly isolates **"Based on your material"** from **"General AI knowledge"**, with summarization, flashcards, and MCQs.
7. **Learning Progress (`/progress`):** Visual mastery tracking, subject distribution, and recommended study sequence pathways.
8. **Doubt History (`/history`):** Complete repository of previous questions with search, subject/difficulty filtering, review, and deletion.
9. **Settings (`/settings`):** Student preference configuration, default academic levels, and live Gemini API health status.

---

## 🧠 4. Gemini API Integration Architecture

Gemini is the central intelligence engine across all modules:

| Feature | Gemini Function / Prompt | Output Schema |
|---|---|---|
| **Doubt Analysis & Solution** | `buildAnalyzeAndSolvePrompt` | 10-part structured JSON (Subject, Topic, Misconception, Analogy, Steps, Code/Math, Exam Structure) |
| **Multimodal Vision** | `generateGeminiContent` with `inlineData` | Visual OCR, diagram parsing, handwritten formula resolution |
| **Adaptive Explanations** | `buildAdaptiveExplanationPrompt` | Simpler (metaphors), Normal (academic), Deeper (compiler/proofs) |
| **Follow-Up Context** | `buildFollowUpPrompt` | Threaded context preservation with follow-up insights |
| **Practice Generation** | `buildPracticeGenerationPrompt` | Targeted MCQ, Short Answer, Numerical, or Code challenges |
| **Socratic Evaluation** | `buildPracticeEvaluationPrompt` | Score (0-100), exact mistake analysis, optimal approach |
| **Interactive "Teach Me"** | `buildTeachMePrompt` | Turn-by-turn Socratic check questions and dynamic feedback |
| **Study Material Q&A** | `buildStudyMaterialPrompt` | Grounded source citations vs general AI knowledge separation |
| **Learning Sequences** | `buildRecommendationPrompt` | Diagnostic learning curve and prerequisite-to-mastery paths |

### Security & Key Protection
- The `GEMINI_API_KEY` is accessed **strictly on the server side** in Next.js Route Handlers.
- It is **never** exposed to frontend bundles, client-side React code, or `NEXT_PUBLIC_*` variables.
- Multi-model failover automatically routes requests across candidate models with automatic retry on transient high-demand spikes (503).

---

## ⚡ 5. Quick Start & Local Run

### Prerequisites
- Node.js 18+ or 20+
- npm or yarn or pnpm
- Google Gemini API Key ([Google AI Studio](https://aistudio.google.com/))

### Step 1: Clone or navigate to the project directory
```bash
cd ai-doubt-solver
```

### Step 2: Install dependencies
```bash
npm install
```

### Step 3: Configure Environment Variables
Copy `.env.example` to `.env.local`:
```bash
cp .env.example .env.local
```
Add your Gemini API Key in `.env.local`:
```env
GEMINI_API_KEY=AIzaSy...your_gemini_api_key_here
GEMINI_MODEL=gemini-3.5-flash
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

### Step 4: Run Live Gemini Verification Suite
Verify real Gemini API reasoning and zero mock responses:
```bash
npm run test:gemini
```
*Output will execute live tests against Google Gemini for doubt solving, misconception detection, adaptive granularity, practice evaluation, Socratic tutoring, and multimodal vision.*

### Step 5: Start Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🗄️ 6. Supabase Database Schema

The complete PostgreSQL database schema with `pgvector` support is available in `supabase/schema.sql`.

### Tables:
1. `profiles`: User account details, academic level, and style preferences.
2. `doubts`: Stored academic questions, input type, detected topics, misconceptions, and 10-part solutions. Includes vector embeddings for semantic search.
3. `doubt_messages`: Threaded follow-up conversations and adaptive explanations.
4. `practice_questions`: AI-generated practice questions and options.
5. `practice_submissions`: Student answers, scores, and Gemini evaluation feedback.
6. `study_materials`: Stored lecture notes, summaries, and generated flashcards.
7. `learning_profiles`: Strong/weak topics and personalized recommendation pathways.

To apply the schema in Supabase:
1. Open your Supabase Project Dashboard.
2. Navigate to the **SQL Editor**.
3. Paste the contents of `supabase/schema.sql` and click **Run**.

---

## 🎯 7. Five Demo Scenarios for Live Hackathon Judging

1. **Demo 1 (Core Doubt & Misconception):**
   - Question: *"Why does Java not support multiple inheritance with classes?"*
   - Result: Gemini detects `Computer Science` → `Java Inheritance`, identifies the Diamond Problem misconception, provides an analogy, and outputs clean Java code using interfaces.
2. **Demo 2 (Multimodal Diagram / Handwritten Math):**
   - Click "Image / Diagram" tab in Ask Doubt and upload an image of a handwritten math problem or screenshot.
   - Result: Gemini vision transcribes the problem, identifies the topic, and resolves it step-by-step.
3. **Demo 3 (Adaptive "Explain Simpler"):**
   - On any solved doubt, click **"Explain Simpler"**.
   - Result: Gemini regenerates a kid-friendly metaphor and non-jargon explanation instantly using the existing context.
4. **Demo 4 (Practice Socratic Evaluation):**
   - Go to `/practice`, generate a question on `Object-Oriented Programming`, and submit a partially flawed answer.
   - Result: Gemini grades the answer out of 100, pinpoints the exact conceptual gap, and recommends the next difficulty.
5. **Demo 5 (Interactive Socratic Tutoring):**
   - Go to `/teach-me`, enter *"DBMS Normalization (1NF, 2NF, 3NF)"*.
   - Result: Gemini starts an interactive step-by-step session, checks understanding after each concept, and dynamically adapts.

---

## ⚖️ 8. Responsible AI Implementation

- **Transparent Disclaimers:** Visible responsible AI banners remind students to cross-verify critical academic formulas with faculty and textbooks.
- **Strict Grounding in Study Material:** The Study Material module explicitly separates "Based on your material" from "General AI knowledge" to eliminate hallucination.
- **No Hidden Chain-of-Thought:** Internal system reasoning remains private, providing students only with constructive, high-level educational explanations.
