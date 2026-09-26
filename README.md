# n8n AI Automations

Practical **n8n automation and AI workflow projects** built to explore triggers, integrations, conditional logic, AI agents, memory, and external tools.

This repository contains three progressively more capable n8n workflows, starting with a simple scheduled automation and progressing toward an AI-powered personal assistant.

---

## Projects

| # | Project                                                                   | Main Concepts                                  |
| - | ------------------------------------------------------------------------- | ---------------------------------------------- |
| 1 | [Daily Weather Email Automation](./project-1-daily-weather/README.md)     | Scheduling, HTTP requests, API data, Gmail     |
| 2 | [Lead / Sponsorship Intake Automation](./project-2-lead-intake/README.md) | Forms, conditional logic, Gmail, Google Sheets |
| 3 | [AI Personal Assistant](./project-3-ai-personal-assistant/README.md)      | AI Agent, LLM, memory, tools, Google services  |

---

## Project 1 — [Daily Weather Email Automation](./project-1-daily-weather/README.md)

A scheduled workflow that retrieves current weather information from the **Open-Meteo API** and sends a daily email through Gmail.

### Workflow

```text
Schedule Trigger
       ↓
HTTP Request
       ↓
Open-Meteo API
       ↓
Gmail
```

### Concepts Demonstrated

* Scheduled workflow execution
* HTTP/API requests
* Reading JSON API responses
* Mapping API data into another service
* Automated Gmail messages

---

## Project 2 — [Lead / Sponsorship Intake Automation](./project-2-lead-intake/README.md)

A form-based workflow for receiving sponsorship or lead inquiries, evaluating the submitted budget, sending an appropriate email response, and recording the result in Google Sheets.

The workflow uses a **1,000,000 budget threshold** to route submissions.

### Workflow

```text
Form Submission
       ↓
Budget Evaluation
       ↓
     Switch
    ↙      ↘
Decline    Approval
   ↓          ↓
 Gmail       Gmail
   ↓          ↓
 Sheets      Sheets
```

### Concepts Demonstrated

* n8n form triggers
* Form data processing
* Conditional routing
* Business rules
* Dynamic email content
* Google Sheets integration
* Recording workflow decisions

---

## Project 3 — [AI Personal Assistant](./project-3-ai-personal-assistant/README.md)

An AI-powered assistant that accepts natural-language requests and uses connected tools to retrieve information from Google Calendar, Gmail, and Google Sheets.

The workflow uses an **AI Agent** with the `openai/gpt-oss-120b` model through Groq and includes short-term conversation memory.

### Workflow

```text
Chat Message
      ↓
   AI Agent
      │
      ├── Groq Chat Model
      ├── Simple Memory
      ├── Google Calendar
      ├── Gmail
      └── Google Sheets
```

The agent decides which tool is relevant to the user's request instead of following a fixed sequence of tool calls.

### Example Requests

```text
What does my calendar look like tomorrow?
```

```text
Summarize my recent emails.
```

```text
Do we have any new sponsorship requests?
```

### Concepts Demonstrated

* AI Agents in n8n
* LLM integration
* Tool calling
* Agent-based tool selection
* Short-term conversation memory
* Google Calendar integration
* Gmail integration
* Google Sheets integration
* Read-only external tools
* Natural-language interfaces

---

## Progression Across the Projects

The three projects demonstrate a progression from traditional workflow automation to AI-powered automation.

```text
Project 1
Simple Automation
      ↓
Triggers + API + Action
      ↓
Project 2
Business Workflow
      ↓
Forms + Logic + Integrations
      ↓
Project 3
AI-Powered Workflow
      ↓
LLM + Agent + Memory + Tools
```

### What Changes?

**Project 1** follows a fixed sequence:

```text
Trigger → Get Data → Send Email
```

**Project 2** introduces explicit business logic:

```text
Input → Evaluate → Route → Action → Record
```

**Project 3** introduces an AI Agent that can decide which connected tool to use:

```text
User Request → AI Agent → Appropriate Tool → Response
```

This progression demonstrates how increasingly flexible automation can be built in n8n.

---

## Technologies Used

* **n8n** — Workflow automation and orchestration
* **Groq** — LLM provider for Project 3
* **GPT-OSS 120B** — AI model used by Project 3
* **Open-Meteo API** — Weather data source
* **Gmail** — Email integration
* **Google Sheets** — Data storage and retrieval
* **Google Calendar** — Calendar data retrieval
* **n8n AI Agent** — Agentic workflow component
* **n8n Simple Memory** — Short-term conversation memory

---

## Repository Structure

The repository is organized into three independent project directories:

```text
.
├── project-1-daily-weather/
├── project-2-lead-intake/
├── project-3-ai-personal-assistant/
├── .gitignore
└── README.md
```

Each project directory contains its corresponding n8n workflow export and project-specific documentation.

---

## Running the Projects

These workflows were built and tested using a **local n8n installation**.

Start n8n with:

```bash
n8n
```

Then open:

```text
http://localhost:5678
```

Import the JSON workflow for the project you want to run.

Each project's README contains its specific setup instructions and required credentials.

---

## Credentials & Configuration

The workflows integrate with external services, so credentials must be configured in your own n8n instance.

Depending on the project, you may need:

* Gmail OAuth2
* Google Sheets OAuth2
* Google Calendar OAuth2
* Groq API credentials

The exported workflows should be reviewed before being committed to a public repository.

Do not commit:

* API keys
* Access tokens
* Refresh tokens
* Passwords
* Private credentials
* Unnecessary private resource identifiers
* Personal test data

Use your own credentials and external resources when importing these workflows.

---

## Security

A public n8n workflow repository should separate workflow logic from private credentials and personal data.

Before publishing workflow exports:

1. Review every JSON workflow file.
2. Remove or sanitize pinned test data.
3. Remove API keys, tokens, passwords, or other secrets.
4. Review Google Calendar and Google Sheets resource identifiers.
5. Avoid publishing private OAuth credential information.
6. Remove personal email addresses or other private test data.
7. Use your own credentials and external resources when importing the workflows.

The supplied Project 3 workflow has an empty `pinData` object. Project 2's exported workflow should be reviewed for pinned test data before being committed publicly.

---

## Learning Goals

These projects were built to practice practical n8n concepts rather than simply use isolated nodes.

The repository covers:

* Workflow triggers
* Scheduled automation
* API integration
* Data mapping
* Forms
* Conditional logic
* External service integrations
* Automated email
* Spreadsheet storage
* AI Agents
* LLM integration
* Tool calling
* Memory
* Natural-language interfaces
* Read-only AI tools
* Connecting AI systems to real-world data

---

## Project Philosophy

The projects intentionally increase in complexity:

```text
Traditional Automation
        ↓
Rule-Based Automation
        ↓
AI-Powered Automation
```

The goal is to understand not only **how to use n8n nodes**, but also how different automation patterns can be combined to build practical systems.

Each workflow is kept focused on a specific concept so that the underlying architecture remains easy to understand and extend.
