# 🏥 HealthBot — AI-Powered Patient Education System

> **Udacity AI Agents with LangGraph | Project 1**  
> Built by **Mahendra Nali** | February 2026

---

## 🎯 Project Overview

HealthBot is a **LangGraph-based multi-node AI workflow** that delivers personalised health education to patients. It searches real-time medical data, generates patient-friendly summaries, conducts adaptive quizzes, and suggests related topics — all in a seamless conversational flow.

**Built for:** MediTech Solutions (fictional healthcare company)  
**Problem solved:** Patients struggle to understand medical conditions, leading to poor treatment adherence and hospital readmissions.

---

## ✨ Features

### Core Workflow (Required)
| Step | Node | Description |
|------|------|-------------|
| 1 | `ask_topic` | Patient enters health topic |
| 2 | `ask_difficulty` | Choose Easy / Medium / Hard |
| 3 | `search` | Tavily real-time medical search |
| 4 | `summarize` | LLM generates patient-friendly summary |
| 5 | `present_summary` | Displays summary to patient |
| 6 | `wait_ready` | Patient confirms readiness |
| 7 | `ask_num_questions` | Choose 1–5 quiz questions |
| 8 | `generate_quiz` | Creates MCQ based on summary |
| 9 | `present_quiz` | Shows question to patient |
| 10 | `get_answer` | Patient answers A/B/C/D |
| 11 | `grade_node` | Grades with explanation + citation |
| 12 | `present_grade` | Shows results |
| 13 | `suggest_related` | Suggests 3 related topics |

### ⭐ Stand-Out Features (All 3 Implemented)
1. **Adaptive Difficulty** — Easy/Medium/Hard dynamically adjusts summary depth and quiz complexity
2. **Multi-Question Quiz Engine** — Loop-back conditional edges support 1–5 questions per session
3. **Related Topic Suggestions** — LLM suggests 3 contextual next topics with one-click switching

---

## 🏗️ Architecture

```
START
  → ask_topic          # User enters topic (or pre-filled from suggestion)
  → ask_difficulty     # Easy / Medium / Hard
  → search             # Tavily API search
  → summarize          # Difficulty-aware LLM summarization
  → present_summary    # Display to patient
  → wait_ready         # Patient confirms readiness
  → ask_num_questions  # Choose 1-5 questions
  → generate_quiz      # Difficulty-aware MCQ generation
  → present_quiz       # Show question
  → get_answer         # Patient answers
  → grade_node         # LLM grades with citation
  → present_grade      # Show results
  → check_more_questions ──→ (loop back if more needed)
  → suggest_related    # Final score + 3 related topics
  → ask_continue       # New topic / suggestion / exit
  → reset OR end
```

**LangGraph State Fields:**
```python
class State(MessagesState):
    topic: str
    search_results: str
    summary: str
    quiz_question: str
    quiz_questions: list
    user_answer: str
    grade: str
    continue_session: bool
    difficulty: str          # easy / medium / hard
    num_questions: int       # 1-5
    current_question_num: int
    related_subjects: list
    correct_answers: int     # tracks score
```

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| AI Workflow | LangGraph 0.2.19 |
| LLM | OpenAI GPT-3.5-turbo |
| Search | Tavily (via LangChain community tool) |
| Orchestration | LangChain 0.2.16 |
| Memory | LangGraph MemorySaver |
| Environment | Jupyter Notebook |

---

## 🚀 Quick Start

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/healthbot-langgraph.git
cd healthbot-langgraph
```

### 2. Install dependencies
```bash
pip install langchain==0.2.16
pip install langchain-openai==0.1.23
pip install langgraph==0.2.19
pip install langchainhub==0.1.21
pip install tavily-python==0.4.0
pip install langchain-community==0.2.16
pip install python-dotenv==1.0.1
```

### 3. Configure API Keys
```bash
# Copy the template
cp config.env.template config.env

# Edit config.env and add your keys:
# OPENAI_API_KEY="sk-proj-..."
# TAVILY_API_KEY="tvly-dev-..."
```

**Get your API keys:**
- OpenAI: https://platform.openai.com/api-keys
- Tavily (FREE - 1000 searches/month): https://app.tavily.com/home

### 4. Run HealthBot
```bash
jupyter notebook Healthbot_project_MahendraNali.ipynb
```
Run all cells. HealthBot will start interactively.

---

## 📸 Sample Session

```
🚀 Starting HealthBot...
👋 Welcome to HealthBot!
What health topic would you like to learn about? fever

📊 Choose difficulty: easy/medium/hard: easy
✅ Difficulty set to: EASY

🔍 Searching for: fever...
✅ Found relevant medical information!

📝 Creating a patient-friendly summary...
════════════════════════════════════════
📋 HEALTH INFORMATION SUMMARY
════════════════════════════════════════
A fever is when your body temperature is higher than normal...
════════════════════════════════════════

How many quiz questions? (1-5): 3
🧠 Generating question 1 of 3...

❓ COMPREHENSION CHECK
Question: What defines a fever?
A) Temperature below 98°F  B) Temperature above normal
C) Feeling cold            D) Low blood pressure

Your answer (A/B/C/D): B

📊 Grade: Correct ✅
Progress: 1/3 | ✅ 1 correct

════════════════════════════════════════
🏆 SESSION COMPLETE!
Topic: FEVER | Difficulty: EASY | Score: 2/3 (67%)
════════════════════════════════════════

💡 Related Topics:
1. Infections: How infections cause fever
2. Immune System: How your body fights fever
3. Fever Management: Home treatment options
```

---

## 📂 Project Structure

```
healthbot-langgraph/
├── Healthbot_project_MahendraNali.ipynb   # Main implementation
├── HealthBot_Project_Presentation.pptx    # Project slides
├── config.env.template                    # API key template (safe)
├── .gitignore                             # Protects config.env
└── README.md                              # This file
```

---

## 🎓 Learning Outcomes

Through this project I learned:

- **LangGraph State Management** — How state flows through nodes and persists across the workflow
- **Conditional Edges** — Routing logic for quiz loops and session continuation
- **Prompt Engineering** — Adapting LLM prompts dynamically based on difficulty level
- **Tool Integration** — Connecting Tavily search via LangChain community tools
- **Human-in-the-loop** — Using Jupyter `input()` for interactive patient interactions
- **Agentic Patterns** — Single-responsibility nodes, clean state resets, error handling

---

## 🔗 Part of My AI/ML Portfolio

This project is part of my transition from **11 years of Cloud Data Engineering** into **AI Agent development**.

**My Background:** AWS | Snowflake | dbt | PySpark | Data Pipelines  
**Learning:** LangGraph | LLMs | RAG | MCP | Agentic Workflows

---

## 📄 License

MIT License — feel free to use and modify for learning purposes.

---

*Completed as part of Udacity's "AI Agents with LangGraph" course*
