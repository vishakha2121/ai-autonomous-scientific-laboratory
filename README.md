# 🧪 AI Autonomous Scientific Laboratory

> An AI-powered autonomous laboratory system where intelligent agents plan experiments, control simulated laboratory robots, analyze results, generate new hypotheses, and publish scientific findings — all without human intervention.

![Status](https://img.shields.io/badge/status-active--development-yellow)
![Python](https://img.shields.io/badge/python-3.10+-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-green)
![React](https://img.shields.io/badge/React-18+-61DAFB)
![Gemini](https://img.shields.io/badge/Gemini-AI-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 📖 Table of Contents

1. [Introduction](#-introduction)
2. [Problem Statement](#-problem-statement)
3. [Solution Overview](#-solution-overview)
4. [Key Features](#-key-features)
5. [System Architecture](#-system-architecture)
6. [Tech Stack](#-tech-stack)
7. [Project Folder Structure](#-project-folder-structure)
8. [How It Works](#-how-it-works)
9. [AI Agents Explained](#-ai-agents-explained)
10. [Bayesian Optimization](#-bayesian-optimization)
11. [Robot Simulation](#-robot-simulation)
12. [Database Schema](#-database-schema)
13. [API Endpoints](#-api-endpoints)
14. [Frontend Pages & UI](#-frontend-pages--ui)
15. [Installation & Setup](#-installation--setup)
16. [Environment Variables](#-environment-variables)
17. [Running the Project](#-running-the-project)
18. [Demo Flow](#-demo-flow)
19. [Screenshots](#-screenshots)
20. [Limitations & Future Scope](#-limitations--future-scope)
21. [Author & Credits](#-author--credits)
22. [License](#-license)

---

## 🧬 Introduction

**AI Autonomous Scientific Laboratory** is a self-driving laboratory simulation where multiple AI agents collaborate to perform the entire scientific research cycle:

- 📝 **Plan** experiments based on a research goal
- 🤖 **Control** virtual laboratory robots
- 🔬 **Execute** experiments in a simulated environment
- 📊 **Analyze** experimental results
- 💡 **Generate** new scientific hypotheses
- 📄 **Publish** findings in structured reports

This project demonstrates how **Large Language Models (LLMs)** like **Google Gemini** can be combined with **classical optimization algorithms (Bayesian Optimization)** and **robotic simulation** to build an **autonomous research pipeline**.

> ⚠️ **Note:** This is a **practice / learning project**, not a production-grade system. It runs entirely on **CPU** using **Gemini API** (no GPU required).

---

## ❗ Problem Statement

Traditional scientific research is:

- ⏳ **Slow** — takes months/years
- 💰 **Expensive** — requires human researchers + equipment
- 🔁 **Repetitive** — many trial-and-error experiments
- 🧠 **Limited** — humans can only test so many hypotheses

**Question:** Can we build a system where AI agents run the entire research loop autonomously?

---

## 💡 Solution Overview

This project builds a **closed-loop autonomous lab**:



Each step is handled by a **specialized AI agent** powered by **Google Gemini**, and experiments are executed in a **virtual lab robot simulator**.

---

## ✨ Key Features

| Feature | Description |
|--------|-------------|
| 🧠 **Multi-Agent System** | 5 specialized AI agents working together |
| 🤖 **Virtual Lab Robot** | Simulated pipette, heater, mixer, sensor |
| 📈 **Bayesian Optimization** | Smart selection of next experiment |
| 🔍 **Auto Hypothesis Generation** | LLM proposes new scientific ideas |
| 📄 **Auto Report Writing** | Publishes structured findings |
| 📊 **Interactive Dashboard** | Live agent activity + charts |
| 🎛️ **Robot Control Panel** | Manual + auto control of lab robot |
| 🌗 **Modern Dark UI** | React + Tailwind + ShadCN components |
| 🔌 **REST API** | FastAPI with auto Swagger docs |
| 💾 **SQLite Database** | Zero-config database for practice |

---

## 🏗 System Architecture



---

## ⚙️ How It Works

### **Step-by-Step Execution Flow**

1. **User creates a research goal**  
   Example: *"Find the optimal catalyst concentration for maximum yield."*

2. **PlannerAgent** (Gemini) breaks the goal into a structured experiment plan.

3. **ExecutorAgent** converts the plan into robot actions (e.g., `pipette(5ml)`, `heat(80°C)`).

4. **RobotSimulator** executes these actions in a virtual lab and returns simulated results.

5. **AnalyzerAgent** (Gemini) analyzes results and extracts insights.

6. **BayesianOptimizer** suggests the next best experiment parameters.

7. **HypothesisAgent** (Gemini) generates new hypotheses based on findings.

8. **PublisherAgent** (Gemini) writes a final report summarizing everything.

9. **Frontend Dashboard** displays live progress, logs, and charts.

---

## 🤖 AI Agents Explained

| Agent | Role | Powered By |
|-------|------|-----------|
| **PlannerAgent** | Converts high-level goal → structured experiment plan | Gemini |
| **ExecutorAgent** | Converts plan → robot action sequence | Rule-based + Gemini |
| **AnalyzerAgent** | Interprets results, finds patterns | Gemini |
| **HypothesisAgent** | Suggests new scientific hypotheses | Gemini |
| **PublisherAgent** | Writes final reports / papers | Gemini |

Each agent has its own **prompt template** stored in `backend/app/prompts/`.

---

## 📈 Bayesian Optimization

To avoid wasting experiments, we use **Bayesian Optimization**:

1. **Gaussian Process (GP)** models the unknown objective function
2. **Expected Improvement (EI)** decides the next point to sample
3. This minimizes the number of experiments needed to find the optimum

**Implementation:** `backend/app/optimization/bayesian_optimizer.py`  
**Library:** `scikit-learn` (GaussianProcessRegressor)

---

## 🤖 Robot Simulation

We simulate a virtual lab robot with these instruments:

| Instrument | Action | Simulation |
|-----------|--------|-----------|
| Pipette | `pipette(volume)` | Returns dispensed volume |
| Heater | `heat(temp, time)` | Returns final temp |
| Mixer | `mix(speed, time)` | Returns mixing efficiency |
| Sensor | `read_sensor()` | Returns measured value |

The simulator adds **random noise** to mimic real-world uncertainty.

**File:** `backend/app/robotics/robot_simulator.py`

---

## 🗄 Database Schema

**Database:** SQLite (`backend/data/lab.db`)

| Table | Columns |
|-------|---------|
| `experiments` | id, title, goal, status, parameters(JSON), created_at, updated_at |
| `hypotheses` | id, text, confidence, source_experiment_id, created_at |
| `agent_logs` | id, agent_name, action, message, timestamp |
| `robot_actions` | id, experiment_id, action_type, params(JSON), status, timestamp |
| `results` | id, experiment_id, metrics(JSON), analysis_text, created_at |
| `publications` | id, title, content, experiment_ids(JSON), created_at |

---

## 🔌 API Endpoints

**Base URL:** `http://localhost:8000/api`

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/experiments` | Create new experiment |
| GET | `/experiments` | List all experiments |
| GET | `/experiments/{id}` | Get experiment details |
| POST | `/experiments/{id}/run` | Run experiment via agents |
| GET | `/hypotheses` | List all hypotheses |
| POST | `/hypotheses/generate` | Generate new hypothesis |
| GET | `/agents/logs` | Get agent activity logs |
| POST | `/robot/execute` | Send robot command |
| GET | `/robot/status` | Get robot status |
| GET | `/results/{experiment_id}` | Get results |
| POST | `/publications/generate` | Generate report |
| GET | `/dashboard/stats` | Dashboard statistics |

**Auto Docs:** `http://localhost:8000/docs` (Swagger UI)

---

## 🎨 Frontend Pages & UI

| Page | Description |
|------|-------------|
| **Dashboard** | Stats cards, live agent feed, running experiments |
| **Experiments** | List + filter + create |
| **Experiment Detail** | Timeline, robot actions, results chart |
| **Hypotheses** | AI-generated ideas with confidence badges |
| **Robot Control** | Live SVG lab view + manual controls |
| **Results** | Charts + data tables |
| **Publications** | Generated reports |
| **Settings** | Theme, API config |

**UI Theme:** Dark mode + neon green/blue accents + glassmorphism cards

---

## 🚀 Installation & Setup

### **Prerequisites**
- Python 3.10+
- Node.js 18+
- Gemini API Key ([Get it here](https://aistudio.google.com/app/apikey))

### **Backend Setup**
```bash
cd backend
python -m venv venv
venv\Scripts\activate       # Windows
# source venv/bin/activate  # Linux/Mac
pip install -r requirements.txt