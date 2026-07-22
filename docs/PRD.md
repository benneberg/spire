# ============================================================
# 1. PRD.md
# ============================================================
prd_content = """# Spire — Personal AI Workspace

## Product Requirements Document

**Version:** 1.0  
**Status:** Final v1 Specification  
**Document Type:** Product Requirements Document

---

## 1. Product Overview

### 1.1 Product Name

Spire

### 1.2 Product Type

Local-first Personal AI Workspace.

### 1.3 Product Vision

Spire helps individuals transform information, projects, and expertise into reusable knowledge and high-quality artifacts through structured AI workflows.

Spire is not designed around conversations. It is designed around:

```
Workspace
    +
Project
    +
Workflow
    +
Context
    +
Task
    =
Artifact
```

The goal is to create a personal environment where knowledge compounds over time.

---

## 2. Problem Statement

Current AI tools have several limitations:

### Disposable Intelligence
Most AI conversations disappear after completion. Useful outputs are lost inside chat history.

### Repeated Prompt Engineering
Users repeatedly recreate instructions for the same tasks. Examples:
- "Review my code securely"
- "Create documentation"
- "Analyze architecture"
- "Improve accessibility"

The expertise exists only as temporary prompts.

### Fragmented Project Knowledge
Project information is distributed across repositories, documents, notes, chats, cloud storage, and personal files. AI rarely has a complete understanding of the project.

### Lack of Reusable Workflows
AI models are powerful but inconsistent without structured processes. A good result requires expertise definition, quality standards, expected outputs, and context selection. Spire solves this through workflows.

---

## 3. Target User

### Primary User
A technical creator who:
- Develops software
- Designs systems
- Writes documentation
- Researches technologies
- Plans products
- Creates structured deliverables

**Examples:** software developers, indie hackers, technical founders, architects, researchers, engineers.

---

## 4. Product Goals

### Goal 1 — Create a Personal AI Workspace
Users should have one place for projects, workflows, tasks, artifacts, and knowledge.

### Goal 2 — Make AI Expertise Reusable
Users should create workflows that represent specialized capabilities. Examples:
- Security Auditor
- Production Readiness Reviewer
- Marketing Strategist
- Architecture Designer
- Documentation Expert

### Goal 3 — Create Durable Outputs
AI output should become reusable artifacts. Examples:
- Markdown documents
- Reports
- Checklists
- Architecture diagrams
- Specifications
- Plans

### Goal 4 — Maintain User Ownership
Users own their data, API keys, projects, workflows, and artifacts. No mandatory cloud dependency.

---

## 5. Core Concepts

### Workspace
The complete Spire environment. Contains: Projects, Workflows, Tasks, Artifacts, Conversations, Knowledge, Providers, Settings.

### Project
A collection of information related to a goal. Examples: Application, Product idea, Research topic, Business plan. A project may contain URLs, Files, Source code, Notes, and Generated artifacts.

### Workflow
A reusable AI capability. A workflow defines: Role identity, Expertise, Process, Quality rules, Expected outputs, Preferred models. Workflows replace traditional AI personas.

### Task
A specific execution request. Example:
- **Project:** Mobile Banking App
- **Workflow:** Security Auditor
- **Task:** Perform authentication security review

### Artifact
The durable result of a task. Examples: Security report, README, PRD, Architecture document. Artifacts are editable, versioned, exportable, and searchable.

---

## 6. Functional Requirements

### 6.1 Workspace Management
The system must support:
- Creating a workspace
- Exporting workspace data
- Importing workspace backups
- Searching workspace content

### 6.2 Project Management
Users must be able to:
- Create projects with: Name, Description, Tags, Notes
- Add project inputs: Text, URLs, Files, ZIP archives, Source code
- Edit and delete projects
- View project history

### 6.3 Workflow Management
Users must be able to:
- Create workflows
- Edit workflows
- Duplicate workflows
- Version workflows
- Import/export workflows
- Favorite workflows
- Organize workflows by category

### 6.4 Task Execution
Users must be able to:
- Create a task by selecting: Project, Workflow, Deliverable type, AI provider, Model
- Provide a request
- Preview generated context
- Execute task
- Receive streamed results
- Review generated artifact

### 6.5 Artifact Management
Artifacts must support:
- Creation
- Editing
- Versioning
- Comparison
- Export
- Linking to originating task

Artifact metadata must include: Workflow used, Model used, Date created, Project relationship.

### 6.6 AI Provider Support

**Version 1 must support:**

**Groq**
- Purpose: Fast inference, daily assistance, simple tasks

**OpenRouter**
- Purpose: Model selection, reasoning models, specialized tasks

**Future-compatible providers:**
- OpenAI
- Anthropic
- Gemini
- Ollama
- LM Studio

### 6.7 GitHub Integration

**Version 1 design requirement:** Support optional GitHub authentication storage.

**Initial capabilities:**
- Connect GitHub account
- Import repositories
- Read repository contents
- Use repository files as project inputs

**Restrictions:**
- No write access
- No commits
- No pull requests

Future versions may expand capabilities.

---

## 7. Version 1 Feature Scope

### Included

**Workspace**
- ✅ Local storage
- ✅ Export/import

**Projects**
- ✅ CRUD
- ✅ Files
- ✅ URLs
- ✅ Code input

**Workflows**
- ✅ Workflow library
- ✅ Workflow editor
- ✅ Versioning

**AI**
- ✅ Groq
- ✅ OpenRouter
- ✅ Streaming responses
- ✅ Prompt generation

**Context**
- ✅ Context assembly
- ✅ Token management
- ✅ Context preview

**Tasks**
- ✅ Task execution
- ✅ Execution history

**Artifacts**
- ✅ Creation
- ✅ Editing
- ✅ Versioning
- ✅ Export

---

## 8. Explicit Non-Goals for v1

The following are intentionally postponed:

### Autonomous Agents
- No background agents
- No autonomous loops
- No unrestricted actions

### Multi-user Collaboration
- No teams
- No permissions
- No sharing accounts

### Advanced Retrieval
- No embeddings
- No vector database
- No semantic search

### Automation
- No scheduled tasks
- No recurring workflows

### Cloud Platform
- No mandatory servers
- No subscriptions
- No hosted workspace

---

## 9. Success Criteria

Spire v1 succeeds when a user can:
1. Create a project
2. Add project information
3. Select a workflow
4. Create a task
5. Generate an artifact
6. Review the result
7. Edit and version it
8. Export the workspace
9. Restore the workspace successfully

---

## 10. Product Quality Requirements

### Reliability
The application should never lose user data.

### Transparency
Users should understand:
- What model was used
- What context was provided
- How the result was generated

### Performance
The application should feel instant for:
- Navigation
- Searching
- Editing
- Local operations

### Privacy
External communication only occurs when:
- User selects an AI provider
- User sends a request

No hidden data transmission.

---

## 11. Final Product Definition

Spire is a personal AI workspace where:

- **Projects** provide context.
- **Workflows** provide expertise.
- **Tasks** provide intent.
- **AI** provides generation.
- **Artifacts** preserve knowledge.

The workspace becomes more valuable with every completed task.
"""

