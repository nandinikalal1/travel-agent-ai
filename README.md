# Travel Agent AI using LangGraph

Travel Agent AI is a multi-agent AI travel planning application built using LangGraph.

The system uses four specialized agents that work together to search for travel information, find hotels, build an itinerary, and generate a complete travel plan.

## Features

- ✈️ Flight Search Agent
- 🏨 Hotel Search Agent
- 🗓️ Itinerary Planning Agent
- 🤖 Final Response Agent
- 🧠 Persistent conversation memory using PostgreSQL
- 🌐 Real-time API integration
- 💻 Streamlit web interface

---

## Tech Stack

- Python
- LangGraph
- LangChain
- Groq
- PostgreSQL
- Streamlit
- Tavily API
- AviationStack API
- Psycopg

---

## Multi-Agent Workflow

```text
User Request
     ↓
Flight Agent
     ↓
Hotel Agent
     ↓
Itinerary Agent
     ↓
Final Response Agent
     ↓
Travel Plan
```

PostgreSQL is used by the LangGraph checkpointer to persist conversation and workflow state.

---

## Project Structure

```text
travel-agent-ai/
│
├── main.py
├── frontend.py
├── .env
├── .gitignore
│
├── tools/
│   ├── flight_tool.py
    └── tavily_tool.py

```

> `.env` is excluded from Git and should never be committed to the repository.

---

## Installation

### 1. Clone the repository

```bash
git clone YOUR_REPOSITORY_URL
cd travel-agent-ai
```

### 2. Create a virtual environment

```bash
python3 -m venv langgraph_env3
```

Activate it on macOS/Linux:

```bash
source langgraph_env3/bin/activate
```

### 3. Install dependencies

```bash
pip install langgraph langchain langchain-openai langchain-groq langchain-community langchain-tavily "psycopg[binary,pool]" python-dotenv tavily-python requests streamlit langgraph-checkpoint-postgres
```

---

## Environment Variables

Create a `.env` file in the root project directory:

```text
travel-agent-ai/
├── .env
├── main.py
├── frontend.py
└── tools/
```

Add:

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
AVIATIONSTACK_API_KEY=your_aviationstack_api_key
DATABASE_URL=your_postgresql_connection_url
```

Do not commit the `.env` file or expose real API keys, database passwords, or other credentials.

---

## API Keys

You will need API credentials for:

- Groq
- Tavily
- AviationStack

---

## PostgreSQL

Create a PostgreSQL database for LangGraph memory and configure its connection URL through `DATABASE_URL` in `.env`.

LangGraph's PostgreSQL checkpointer creates the required checkpoint tables when the application initializes.

---

## Run the Application

### Terminal

```bash
python3 main.py
```

Enter a travel request when prompted.

Example:

```text
Plan a one-month trip from Seattle to Hyderabad, India.
```

### Streamlit Web Application

```bash
streamlit run frontend.py
```

Open the local Streamlit URL displayed in the terminal.

---

## How It Works

1. The user enters a travel request.
2. The Flight Agent searches for flight information.
3. The Hotel Agent searches for hotel information.
4. The Itinerary Agent generates a structured travel itinerary.
5. The Final Response Agent combines the results into a complete travel plan.
6. LangGraph coordinates the agent workflow.
7. PostgreSQL persists LangGraph conversation and workflow state.

---

## Architecture

```text
                    Travel Request
                          │
                          ▼
                   ┌──────────────┐
                   │ Flight Agent │
                   └──────┬───────┘
                          │
                          ▼
                   ┌─────────────┐
                   │ Hotel Agent │
                   └──────┬──────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │ Itinerary Agent │
                 └────────┬────────┘
                          │
                          ▼
                  ┌─────────────┐
                  │ Final Agent │
                  └──────┬──────┘
                         │
                         ▼
                 Complete Travel Plan

                         ↕
              PostgreSQL Checkpointer
```