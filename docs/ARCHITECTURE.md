# ============================================================
# 2. ARCHITECTURE.md
# ============================================================
architecture_content = """# Spire — Personal AI Workspace

## Architecture Specification

**Version:** 1.0  
**Status:** Final v1 Architecture Specification

---

## 1. Architecture Overview

Spire is designed as a local-first application with a modular AI execution architecture.

The system separates:
- User interface
- Application logic
- Workspace data
- AI orchestration
- External providers

The architecture is designed around one central principle:

> **AI is a capability inside Spire, not the foundation of Spire.**

The workspace, assets, projects, workflows, and artifacts remain valuable regardless of which AI provider is used.

---

## 2. High-Level Architecture

```
┌──────────────────────────────┐
│          User Interface       │
│                              │
│  Dashboard                   │
│  Projects                    │
│  Tasks                       │
│  Workflows                   │
│  Artifacts                   │
│  Settings                    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     Application Services      │
│                              │
│  Workspace Service           │
│  Project Service             │
│  Task Service                │
│  Artifact Service            │
│  Workflow Service            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        AI System Layer        │
│                              │
│  Context Engine              │
│  Prompt Builder              │
│  Task Runner                 │
│  Execution Logger            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       Provider Layer          │
│                              │
│  Groq                        │
│  OpenRouter                  │
│  Future Providers            │
└──────────────────────────────┘
```

---

## 3. Architectural Principles

### 3.1 Local First
The default assumption: User data belongs locally.

The application should function without:
- Accounts
- Cloud services
- External databases

External communication only occurs when explicitly requested.

### 3.2 Modular Services
Each major capability should exist as an independent service.

Examples:
- `ProjectService`
- `ArtifactService`
- `WorkflowService`
- `TaskService`
- `ProviderService`
- `ContextService`

Services communicate through defined interfaces.

### 3.3 Provider Independence
Spire must not depend on one AI vendor.

The workflow system should not know whether execution happens through:
- Groq
- OpenRouter
- OpenAI
- Local models

All providers implement a shared interface.

### 3.4 Data Ownership
All important data must be:
- Exportable
- Portable
- Understandable
- Versioned where necessary

---

## 4. Recommended Technology Stack

The architecture supports multiple implementations.

### Recommended v1 implementation:

**Frontend**
- React
- TypeScript
- Tailwind CSS

**Purpose:** Component architecture, strong typing, maintainability

**State Management**
- Recommended: lightweight application state store
- Responsibilities: UI state, active workspace, selections, temporary execution state
- Persistent data should not live only in memory.

**Local Storage**
- Recommended: IndexedDB
- Purpose: Large local datasets, structured storage, offline operation
- Suggested helper: Dexie.js

**File Storage**
Large files should be stored separately from metadata.

Example:
- **Database:** Project metadata, Artifact metadata, Workflow definitions
- **File Storage:** Source files, Documents, Images, Archives

---

## 5. Application Layers

### 5.1 UI Layer
Responsible for:
- Rendering interfaces
- User interaction
- Displaying state

Should not contain:
- AI logic
- Database logic
- Prompt construction

Examples:
- `ProjectView`
- `WorkflowEditor`
- `ArtifactViewer`
- `TaskRunner`
- `SettingsView`

### 5.2 Application Service Layer
Contains business logic.

Examples:

**Project Service**
- Responsibilities: Create project, Update project, Manage inputs, Link artifacts

**Workflow Service**
- Responsibilities: Load workflows, Validate workflows, Version workflows, Manage workflow library

**Task Service**
- Responsibilities: Create tasks, Execute tasks, Store results, Connect artifacts

**Artifact Service**
- Responsibilities: Create artifacts, Version artifacts, Compare versions, Export artifacts

### 5.3 AI System Layer
The AI system is composed of four major components.

**Context Engine**
- **Purpose:** Transform workspace information into a focused context package.
- **Inputs:** Project data, Selected files, Previous artifacts, Workflow requirements, User request
- **Output:** `ContextBundle`
- **Responsibilities:** Relevance selection, Token budgeting, Context ordering, Context preview

**Prompt Builder**
- **Purpose:** Create the final model request.
- **Input:** Workflow + ContextBundle + User Request
- **Output:** AI Prompt
- The prompt should always be inspectable.

**Task Runner**
- **Purpose:** Execute AI tasks.
- **Responsibilities:** Load workflow, Build context, Generate prompt, Select provider, Stream response, Create artifact, Save execution metadata

**Execution Logger**
- Stores: Provider, Model, Timestamp, Prompt, Context snapshot, Token usage, Latency
- **Purpose:** Reproducibility and debugging.

---

## 6. Provider Architecture

All AI providers implement a common interface.

```typescript
interface AIProvider {
  id: string;
  name: string;

  getModels(): Promise<ModelInfo[]>;

  complete(request: AIRequest): Promise<AIResponse>;

  stream(request: AIRequest): AsyncGenerator<string>;
}
```

### Provider Examples

**Groq Provider**
- Optimized for: Speed, Daily usage, Quick iterations

**OpenRouter Provider**
- Optimized for: Model choice, Advanced reasoning, Specialized workflows

---

## 7. Security Architecture

### API Keys
API keys must:
- Never be hardcoded
- Never be included in exports by default
- Never be exposed in logs

### GitHub Token
GitHub authentication must:
- Use minimal permissions
- Default to read-only
- Remain isolated from AI providers

GitHub data should only be transmitted to AI providers when included in an explicit user request.

---

## 8. Workspace Export Architecture

A workspace export should be portable.

```
workspace.spire/
├── workspace.json
├── projects/
│   ├── project-001.json
│   └── files/
├── workflows/
│   ├── security-auditor.json
├── artifacts/
│   ├── artifact-001.md
└── settings.json
```

Sensitive credentials are excluded unless explicitly requested.

---

## 9. Future Extension Points

The architecture intentionally supports future expansion.

### Knowledge Engine
- Future: Embeddings, Semantic search, Automatic linking

### Workflow Execution Graphs
- Future: Multi-step workflows with subagents

### Plugin System
- Future: External capabilities (GitHub, Jira, Notion, Google Drive, MCP tools)

### Desktop Packaging
- Future: The application can be packaged using Tauri, Electron, or native wrappers without changing the core architecture.

---

## 10. Recommended Source Structure

```
src/
  components/
  features/
    workspace/
    projects/
    workflows/
    tasks/
    artifacts/
    settings/
  services/
    projectService
    workflowService
    taskService
    artifactService
  ai/
    contextEngine
    promptBuilder
    taskRunner
  providers/
    groq
    openrouter
  storage/
  types/
  utils/
```

---

## 11. Architecture Summary

Spire is built around:

```
Workspace
    ↓
Assets
    ↓
Projects + Workflows
    ↓
Tasks
    ↓
Context Engine
    ↓
AI Providers
    ↓
Artifacts
    ↓
Knowledge Accumulation
```

The architecture intentionally keeps AI replaceable while making the user's accumulated knowledge permanent.
"""

