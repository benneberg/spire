# spire
Collect any information of your application - take it anywhere. Ai-assisted tools to make it anywhere on your journey 



# AI Project Assistant

A fully self-contained, browser-based AI assistant for developers, designers, and product teams to manage projects, enrich them with AI insights, and chat contextually using Groq’s ultra-fast LLMs.

## 🚀 Features

- **Multi-modal Project Input**: Add multiple URLs, upload files (including ZIPs), and paste raw code—all in one project.
- **AI-Powered Project Inspection**: Request AI to:
  - Summarize the app
  - Generate a technical description
  - Categorize the project
  - Produce a structured `app.json` (title, description, category, tags, technologies, etc.)
- **Editable Artifacts**: View, edit, and save AI-generated outputs directly in the UI.
- **CRUD AI Experts**: Create, edit, or delete role-based AI personas with:
  - Structured prompt templates (role, domain, objectives)
  - Per-role LLM settings (temperature, max tokens)
  - Custom quick actions
- **Context-Aware Chat**: Select any enriched project during chat—AI uses **both raw inputs (URLs/files/code) AND enriched metadata**.
- **Export & History**: Save, delete, or export chats as TXT, JSON, or HTML (for PDF).
- **Live Groq Integration**: Fetch and select from real-time available models.
- **Zero Backend**: All data stored in `localStorage`.

## 🛠️ Tech Stack

- **Frontend**: Vanilla HTML/CSS/JS
- **Styling**: Tailwind CSS (via CDN)
- **Libraries**:
  - `axios` – HTTP client for Groq API
  - `JSZip` – ZIP file parsing
- **Storage**: `localStorage` (no server required)
- **AI Backend**: [Groq API](https://groq.com)

## ▶️ How to Use

1. Open `index.html` in a modern browser.
2. Go to **Settings** → Enter your Groq API key.
3. Add a **Project** (URLs, files, code).
4. **Inspect** the project → Select AI tasks → Submit → Edit results.
5. Go to **Chat** → Choose an **Expert** and a **Project** → Start chatting!

> 💡 No build step. No dependencies. Just one HTML file.

## 🔮 Future Improvements

- **Cloud Sync**: Optional Firebase or Supabase backend for cross-device sync.
- **AI-Assisted Expert Creation**: “Ask AI to generate a new expert” button.
- **Project Versioning**: Track changes to enriched artifacts over time.
- **PWA Support**: Installable app with offline caching.
- **Multi-Model Comparison**: Run the same query across multiple LLMs.
- **Team Sharing**: Export/import projects with full context.
- **Dark Mode Toggle**: User-selectable theme.
- **Voice Input**: Speech-to-text for chat.
- **Automated Testing**: Generate unit tests from code context.

---
Made with ❤️ for builders who want AI that *understands their project*.





# AI Project Assistant – Full Specification for LLM Regeneration

## Goal
Generate a single HTML file that implements a browser-based AI assistant for managing software projects with Groq LLM integration.

## Core Requirements

### 1. **Tabs**
- Settings | Projects | Chat

---

### 2. **Settings Tab**
- **Groq API Key**: Input field, saved to `localStorage`.
- **Model Selector**: Fetch live models from `GET https://api.groq.com/openai/v1/models` using the API key.
- **Global LLM Settings**: Temperature (slider), Max Tokens (number), Machine Prompt (textarea).
- **AI Experts (Roles) CRUD**:
  - Each expert has: `id`, `name`, `domainDescription`, `keyObjectives`, `temperature`, `maxTokens`, `quickActions[]`.
  - **Prompt is auto-generated** from a structured template (see below).
  - Edit/Delete modal with form.
  - Default experts: React Developer, SEO Specialist, Product Manager.
  - Quick actions appear as buttons in Chat.

#### Structured Prompt Template
