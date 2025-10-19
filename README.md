# spire
Collect any information of your application - take it anywhere. Ai-assisted tools to make it anywhere on your journey 



# AI Project Assistant

A fully self-contained, browser-based AI assistant for developers, designers, and product teams to manage projects, enrich them with AI insights, and chat contextually using Groq’s LLMs.

## 🚀 Features

- **Multi-modal Project Input**: Add multiple URLs, upload files (including ZIPs), and paste raw code—all in one project.
- **AI-Powered Project Inspection**: Request AI to:
 - Summarize the app
 - Generate a technical description
 - Categorize the project
 - Produce a structured `app.json` (title, description, tags, category, technologies, etc.)
- **CRUD AI Experts**: Create, edit, or delete role-based AI personas with custom prompts, temperature, max tokens, and quick actions.
- **Context-Aware Chat**: Select any enriched project during chat—AI uses **both raw inputs (URLs/files/code) AND enriched metadata**.
- **Export & History**: Save, delete, or export chats as TXT, JSON, or HTML (for PDF).
- **Full Settings**: API key, live Groq model list, per-role LLM tuning.
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
4. **Inspect** the project → Select AI tasks → Submit.
5. Go to **Chat** → Choose an **Expert** and a **Project** → Start chatting!

💡 No build step. No dependencies. Just one HTML file.



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
 - Each expert has: `id`, `name`, `prompt`, `temperature`, `maxTokens`, `quickActions[]`.
 - Edit/Delete modal with form.
 - Default experts: General, Developer, Designer, Marketing, Creative.
 - Quick actions appear as buttons in Chat.

---

### 3. **Projects Tab**
- Input fields:
 - **URLs**: Textarea (one per line).
 - **File Upload**: Accept multiple files or ZIPs (extract contents).
 - **Manual Code**: Textarea.
- On “Add Project”:
 - Store: `id`, `urls[]`, `files[{name, content}]`, `code`, `createdAt`, `enriched: null`.
- Display list of projects as cards.
- Click a project → open **Project Detail Modal**.

#### Project Detail Modal
- Shows raw inputs (URLs, file names, code snippet).
- Checkboxes for AI tasks:
 - [ ] Summarize app
 - [ ] Technical description
 - [ ] Categorize
 - [ ] Generate app.json
- “Submit” saves selected tasks into `project.enriched = { tasks, analyzedAt }`.

---

### 4. **Chat Tab**
- **Chat History Sidebar**:
 - List of chats with title, message count, duration, preview.
 - “+” for new chat, “📤” to export.
- **Main Chat Area**:
 - **Expert Selector**: Populated from AI Experts.
 - **Project Selector**: Lists all projects.
 - **Quick Actions**: Dynamically loaded from selected expert.
 - **Chat Box**: User/AI messages styled differently.
 - **Stats Panel**: Messages, tokens used, duration.
- On send:
 - Construct prompt: `expert.prompt + "\n\nContext:\n" + projectContext + "\nUser: " + message`
 - `projectContext` includes:
   - All URLs
   - All file contents (truncated to 500 chars)
   - Manual code
   - `project.enriched` (if exists, as JSON)
 - Call Groq API with expert-specific `temperature` and `maxTokens`.
- **Export Modal**: Choose format (txt/json/html), filename, download.

---

### 5. **Persistence**
- All data stored in `localStorage`:
 - `groqApiKey`, `groqModel`, `groqTemp`, `groqMaxTokens`, `groqPrompt`
 - `aiExperts` (array)
 - `aiProjects` (array)
 - `aiChatHistory` (array)

---

### 6. **UI/UX**
- Clean, responsive layout using Tailwind CSS (via CDN).
- Modals for expert/project management.
- No external build tools—single HTML file.

---

### 7. **Libraries (CDN)**
- Tailwind CSS
- Axios
- JSZip

---
