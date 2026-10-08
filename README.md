# 🤖 Personal AI Assistant — n8n

An action-driven **Personal AI Assistant** built with **n8n**, designed to understand natural-language requests and perform everyday productivity tasks through connected tools.

The assistant acts as a centralized interface for **Gmail, Google Calendar, Google Tasks, Google Docs, Google Sheets, and web search**.

> **Goal:** Turn natural-language requests into reliable actions instead of simply generating text.

---

## ✨ What Can It Do?

### 🔎 1. Information & Web Search

The assistant can answer general questions and use web search when current or external information is required.

**Examples:**

```text
"What's the weather going to be like tomorrow?"

"Search for the latest news about NVIDIA."

"Who is the current CEO of OpenAI?"

"Explain how RAG works."
```

It avoids using web search for personal data such as emails, calendar events, or tasks.

---

### 📅 2. Google Calendar Management

The assistant can manage calendar events using Google Calendar.

**Capabilities:**

- Create calendar events
- Retrieve details of a specific event
- Retrieve multiple events
- Check upcoming meetings or events

**Examples:**

```text
"Schedule a meeting with Rahul tomorrow at 3 PM for 30 minutes."

"What meetings do I have today?"

"Show me my events for this week."

"Get the details of my 2 PM meeting."
```

The assistant asks for missing information only when it is required to complete the action.

---

### 📧 3. Gmail Management

The assistant can interact with Gmail for reading and sending messages.

**Capabilities:**

- Read multiple emails
- Read a specific email
- Summarize emails
- Send new emails
- Reply to emails

**Examples:**

```text
"Summarize my unread emails."

"Show me my latest emails."

"Read the email from Rahul."

"Reply to this email saying I'll attend the meeting."

"Send an email to my professor saying I'll submit the assignment tomorrow."
```

Email responses are drafted in a concise and professional style.

---

### ✅ 4. Google Tasks / To-Do Management

The assistant can manage personal tasks and to-do items.

**Capabilities:**

- Create tasks
- Retrieve a single task
- Retrieve multiple tasks
- Delete tasks when explicitly requested

**Examples:**

```text
"Remind me to finish my ML assignment."

"Create a task to apply for internships."

"Show me my pending tasks."

"Delete the task I just completed."
```

Tasks are not deleted automatically unless the user explicitly requests deletion or clearly indicates that the task has been completed.

---

### 📝 5. Notes Management

The assistant uses Google Docs as a notes system.

**Capabilities:**

- Create new notes documents
- Add information to existing notes
- Read notes
- Maintain structured notes

**Examples:**

```text
"Create notes for today's ML lecture."

"Add this to my project notes."

"Show me my notes about LangGraph."

"Append this idea to my AI project notes."
```

Existing notes are **appended to rather than overwritten**.

---

### 💰 6. Expense Tracking

The assistant can use Google Sheets to maintain and analyze expense records.

**Capabilities:**

- Add new expenses
- Retrieve expense history
- Calculate totals
- Calculate summaries
- Perform budget-related calculations

**Examples:**

```text
"Add ₹250 for lunch to my expenses."

"How much did I spend this month?"

"Show me my recent expenses."

"How much have I spent on food?"

"Calculate my total expenses for this week."
```

Arithmetic operations are handled through the calculator tool rather than being estimated by the AI.

---

# 🧠 How It Works

The workflow is built around an **AI Agent** inside n8n.

```text
User Request
     │
     ▼
  Webhook
     │
     ▼
  AI Agent
     │
     ├── Groq Chat Model
     ├── Simple Memory
     │
     ├── Web Search
     │
     ├── Gmail Tools
     │     ├── Get Messages
     │     ├── Get Single Message
     │     └── Send Message
     │
     ├── Calendar Tools
     │     ├── Create Event
     │     ├── Get Single Event
     │     └── Get Events
     │
     ├── Task Tools
     │     ├── Create Task
     │     ├── Get Single Task
     │     ├── Get Multiple Tasks
     │     └── Delete Task
     │
     ├── Notes Tools
     │     ├── Create Notes
     │     ├── Update Notes
     │     └── Get Notes
     │
     └── Expense Tools
           ├── Calculator
           ├── Add Expense
           └── Get Expenses
     │
     ▼
Respond to Webhook
     │
     ▼
    User
```

---

# 🏗️ Workflow Architecture

The current n8n workflow contains the following major components:

| Component | Purpose |
|---|---|
| **Webhook** | Receives user requests |
| **AI Agent** | Understands intent and decides which tool to use |
| **Groq Chat Model** | Provides the LLM reasoning layer |
| **Simple Memory** | Maintains conversational context |
| **Tavily Search** | Provides external web search |
| **Gmail Tools** | Email reading and sending |
| **Calendar Tools** | Calendar and event management |
| **Task Tools** | To-do management |
| **Notes Tools** | Google Docs-based note management |
| **Expense Tracker** | Google Sheets-based expense tracking |
| **Respond to Webhook** | Returns the assistant's response |

---

# 🛠️ Tool Selection

The AI Agent determines which tool is appropriate based on the user's intent.

### Example

User:

> "What meetings do I have tomorrow?"

The agent identifies this as a **calendar request** and uses the calendar events tool.

User:

> "Send Rahul an email saying I'll join at 4 PM."

The agent identifies this as an **email action** and uses Gmail.

User:

> "How much did I spend this month?"

The agent retrieves the relevant expenses and uses the calculator for the total.

User:

> "Search for the latest OpenAI news."

The agent uses web search because the information is current and external.

---

# 🔐 Safety & Reliability Rules

The assistant is designed to prioritize correctness over blindly executing actions.

### Core Rules

- Identify the user's intent before taking action.
- Select the most appropriate tool.
- Do not fabricate tool results or completed actions.
- Ask only for information that is genuinely required.
- Never overwrite existing notes; append instead.
- Do not delete tasks unless explicitly requested or clearly completed.
- Use the calculator for expense totals and calculations.
- Confirm or resolve required event information before creating calendar events.
- Keep email responses concise and professional.
- Do not use web search for personal data such as Gmail, Calendar, or Tasks.
- Clearly state when a request is outside the assistant's capabilities.

---

# 💬 Example Requests

The assistant is designed to understand natural language rather than requiring users to know the underlying tools.

```text
"What's on my calendar today?"

"Schedule a project meeting for Friday at 5 PM."

"Summarize my unread emails."

"Reply to the latest email from my professor."

"Create a task to finish my resume."

"Show me my pending tasks."

"Create a note for my internship work."

"Add ₹120 for metro travel to my expenses."

"How much did I spend this week?"

"Search the web for the latest developments in generative AI."
```

---

# 🔧 Tech Stack

- **n8n** — Workflow automation and orchestration
- **AI Agent** — Intent understanding and tool selection
- **Groq** — LLM provider
- **Gmail** — Email management
- **Google Calendar** — Calendar management
- **Google Tasks** — Task management
- **Google Docs** — Notes management
- **Google Sheets** — Expense tracking
- **Tavily Search** — Web search
- **Webhook** — API-style interface for receiving requests
- **Simple Memory** — Conversation context

---

# 🚀 Project Purpose

This project explores how an LLM can move beyond a traditional chatbot and become an **action-oriented personal assistant**.

Instead of only responding with:

> "You should create a calendar event."

the assistant can actually create the event through an integrated tool.

The same architecture can be extended with additional tools and APIs, allowing the assistant to become a centralized interface for personal productivity and automation.

---

# 🔮 Possible Future Improvements

Potential extensions include:

- WhatsApp or Telegram interface
- Voice input/output
- More advanced long-term memory
- Contact management
- Better email classification
- Automated daily briefings
- Finance dashboards
- Recurring task management
- Reminder and notification workflows
- More robust confirmation flows for sensitive actions
- Authentication and user-specific access control
- Logging and monitoring of agent/tool executions
- Better error handling and retry mechanisms

---

# 📌 Project Status

**Current Status:** Functional n8n-based personal AI assistant with integrated productivity tools.

The project is actively extensible: new capabilities can be added by connecting additional tools to the AI Agent and updating its decision-making instructions.

---

## 👨‍💻 Author

**Ayush Bhardwaj**

B.Tech — Artificial Intelligence & Machine Learning

Focused on **Generative AI, LLMs, Machine Learning, and AI Automation**.