# ============================================================
# 7. UI_UX_SPECIFICATION.md
# ============================================================
ui_ux_content = """# Spire — User Interface & Experience Specification

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. UX Vision

Spire should feel like:
- A modern development environment
- A personal knowledge management system
- An AI production workspace

It should not feel like:
- A chatbot
- A prompt playground
- A collection of disconnected AI tools

The main interaction loop:

```
Create Project
  ↓
Select Workflow
  ↓
Run Task
  ↓
Review Artifact
  ↓
Improve Knowledge
```

---

## 2. Application Layout

Spire uses a desktop application layout.

```
+------------------------------------------------+
| Sidebar                 Main Content            |
|                                                |
| 🏠 Dashboard             Workspace              |
| 📁 Projects                                    |
| ⚡ Tasks                                      |
| 🧠 Workflows                                  |
| 📄 Artifacts                                  |
| ⚙ Settings                                    |
|                                                |
+------------------------------------------------+
```

---

## 3. Global UI Principles

### 3.1 Context Always Visible

The user should always know:

```
Current Project: Smart Home Platform
Current Workflow: Security Auditor
Current Model: Claude Sonnet
Current Task: Authentication Review
```

### 3.2 AI Transparency

AI operations should never feel like magic.

Users can inspect:
- Selected context
- Generated prompt
- Model
- Execution history
- Artifact origin

### 3.3 Progressive Complexity

**Beginner:**
```
Choose Workflow → Describe Goal → Run
```

**Advanced:**
```
Edit Context → Modify Prompt → Select Model → Adjust Parameters
```

---

## 4. Dashboard

**Purpose:** Provide workspace overview.

### Components

**Recent Projects**

Example:
```
Smart Home Controller
Last updated: 2 hours ago
Artifacts: 14
Tasks: 32
```

**Recent Tasks**

```
Security Audit — Completed
Artifact created: Security Report v2
```

**Quick Actions**

Buttons:
- + New Project
- + New Task
- Browse Workflows
- Import Workspace

---

## 5. Projects Screen

**Purpose:** Manage project knowledge.

### Project List

Card layout:

```
---------------------------------
IoT Dashboard
React | Node | MQTT

Artifacts: 12
Last update: Today

Open →
---------------------------------
```

---

## 6. Project Detail Screen

Main knowledge hub.

**Layout:**

```
Project Name

Overview
---------------------------------

Files        Artifacts        Tasks        Notes        Settings
```

### Project Overview

Shows:
- Description
- Technology stack
- Project summary
- Tags
- Statistics

### Files Tab

Features:
- Upload files
- Drag/drop ZIP
- Paste code
- Add URLs

### Artifacts Tab

Shows generated knowledge.

Example:
```
Architecture Document
Version: 3
Created by: Architecture Expert
[Open]
```

### Tasks Tab

Shows project history.

---

## 7. New Task Flow

The most important workflow.

### Step 1 — Select Project

```
Choose project: [ Smart Home Platform ]
```

### Step 2 — Select Workflow

Workflow cards:

```
🛡 Security Auditor
Find vulnerabilities and security risks.

🏗 Production Readiness
Evaluate deployment readiness.

📘 Technical Writer
Create documentation.
```

### Step 3 — Define Goal

Input:
```
What should Spire help you create?

Example: Review whether this application is ready for production.
```

### Step 4 — Context Review

Before execution:

```
AI Context

Included:
✓ Project summary
✓ package.json
✓ Architecture document
✓ Backend files

Excluded:
○ Old discussions
○ Temporary files
```

User can modify.

### Step 5 — Execute

Execution view:

```
Security Auditor
Analyzing...
████████░░
Checking dependencies...
Generating report...
```

---

## 8. Execution View

Split interface:

```
--------------------------------
AI Activity
Analyzing architecture...
Generating findings...

           Artifact Preview
--------------------------------
```

Side panel:

```
Execution Details

Model: Claude Sonnet
Tokens: 8450
Context: 12 files
Workflow: Security Auditor v1
```

---

## 9. Artifact Viewer

Artifacts are first-class.

**Layout:**

```
Artifact Title

Version History
  v1    v2    v3

Content

Actions: [Edit] [Revise] [Export] [Compare]
```

---

## 10. Artifact Editing

v1 supports:
- Markdown editor
- Code editor
- JSON editor

**Future:**
- Collaborative editing
- Rich document editor

---

## 11. Workflow Library

The replacement for "Experts".

### Workflow Browser

Categories:
- Development
- Security
- Business
- Marketing
- Writing
- Design
- Operations

### Workflow Card

Example:

```
🛡 Security Auditor
Category: Security

Creates professional security reviews.

Outputs:
✓ Risk report
✓ Recommendations
✓ Priority checklist

[Use Workflow →]
```

---

## 12. Workflow Detail

Shows:
- Identity
- Instructions
- Quality Standards
- Output Formats
- Model Preferences
- Example Tasks

Advanced users:
- Edit Workflow Definition

---

## 13. Artifact Relationship View

Future-ready.

Example:

```
Project
  |
  + Architecture Document
  |
  + Security Audit
  |
  + API Specification
  |
  + Deployment Plan
```

---

## 14. Settings

### Sections:

**AI Providers**

Supported:
- Groq
- OpenRouter

Future: OpenAI, Anthropic, Gemini, Ollama

Provider card:

```
OpenRouter
Connected ✓
Default reasoning model: Claude Sonnet
```

**GitHub Integration**

Optional v2 preparation.

Settings:
```
GitHub Token: [______________]
Status: Not connected

Connect Repository
```

Security: read-only scopes, encrypted storage

**Appearance**

Options:
- Light/dark mode
- Compact mode
- Animations

---

## 15. Mobile Considerations

v1 target: **Desktop first.**

Responsive support:
- Tablet
- Smaller screens

Not optimized for phone workflows.

---

## 16. Empty States

Every empty screen should guide action.

**Example:**

```
No Projects:

Your workspace is empty.

Create your first project and let Spire understand it.

[Create Project]
```

---

## 17. Keyboard Shortcuts

Future-friendly.

| Shortcut | Action |
|----------|--------|
| Ctrl + K | Open command menu |
| Ctrl + N | New task |
| Ctrl + P | Search projects |

---

## 18. UX Success Criteria

A new user should understand:

| Timeframe | Understanding |
|-----------|--------------|
| Within 30 seconds | "What can I do?" |
| Within 2 minutes | "How do I run an AI workflow?" |
| Within 10 minutes | "How does Spire improve my projects?" |

---

## 19. UI Summary

Spire's core experience:

```
Project
  ↓
Workflow
  ↓
Task
  ↓
Context
  ↓
Execution
  ↓
Artifact
  ↓
Knowledge
```

The UI exists to make this loop effortless.
"""

