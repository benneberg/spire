# ============================================================
# 8. PROJECT_STRUCTURE.md
# ============================================================
project_structure_content = """# Spire — Repository & Code Architecture

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. Development Philosophy

Spire should be built as a modular application.

**Avoid:**
```
components/
  Chat.jsx
  Settings.jsx
  Everything.jsx
```

**Prefer:**
```
features/
  projects/
  workflows/
  tasks/
  artifacts/
```

Each feature owns its:
- Components
- State
- Services
- Types
- Validation

---

## 2. Technology Stack

### Desktop Runtime
- Tauri 2.x
- Rust backend

**Purpose:** Filesystem access, SQLite, secure storage, native integrations

### Frontend
- React
- TypeScript
- Vite
- Tailwind CSS
- Shadcn/UI
- Radix UI

### State Management
- **Global:** Zustand
- **Server/database:** TanStack Query

### Validation
- Zod

### Database
- **Primary:** SQLite
- **Access:** Tauri SQL Plugin

---

## 3. Root Structure

```
spire/
├── src/
├── src-tauri/
├── public/
├── workflows/
├── migrations/
├── tests/
├── package.json
├── README.md
└── docs/
```

---

## 4. Frontend Structure

```
src/
├── app/
├── components/
├── features/
├── hooks/
├── lib/
├── services/
├── stores/
├── types/
├── utils/
├── styles/
└── main.tsx
```

---

## 5. Application Layer

```
src/app/
├── App.tsx
├── router.tsx
├── providers.tsx
└── layout.tsx
```

**Responsibilities:**
- Application startup
- Routing
- Global providers
- Theme

---

## 6. Shared Components

```
src/components/
├── ui/
├── dialogs/
├── editor/
├── markdown/
├── cards/
└── layout/
```

**Examples:**
- Modal
- Button
- ArtifactCard
- WorkflowCard
- FileUploader

---

## 7. Feature Architecture

Each feature follows:

```
feature/
├── components/
├── hooks/
├── services/
├── store.ts
├── types.ts
└── schemas.ts
```

---

## 8. Projects Feature

```
features/projects/
├── components/
│   ├── ProjectCard.tsx
│   ├── ProjectList.tsx
│   ├── ProjectEditor.tsx
├── services/
│   └── projectService.ts
├── hooks/
│   └── useProjects.ts
├── types.ts
└── schemas.ts
```

**Responsibilities:**
- CRUD projects
- Manage inputs
- Project metadata

---

## 9. Workflow Feature

```
features/workflows/
├── components/
│   ├── WorkflowCard.tsx
│   ├── WorkflowBrowser.tsx
├── services/
│   └── workflowService.ts
├── loader.ts
├── types.ts
└── schemas.ts
```

**Responsibilities:**
- Load workflows
- Edit workflows
- Version workflows

---

## 10. Task Feature

```
features/tasks/
├── components/
│   ├── TaskCreator.tsx
│   ├── TaskExecution.tsx
│   ├── TaskHistory.tsx
├── services/
│   └── taskService.ts
├── executor.ts
├── types.ts
└── schemas.ts
```

**Responsibilities:**
- Create tasks
- Execute workflows
- Monitor status

---

## 11. Artifact Feature

```
features/artifacts/
├── components/
│   ├── ArtifactViewer.tsx
│   ├── ArtifactEditor.tsx
│   ├── VersionHistory.tsx
├── services/
│   └── artifactService.ts
├── types.ts
└── schemas.ts
```

**Responsibilities:**
- Storage
- Editing
- Versioning
- Exporting

---

## 12. Context Engine

**Important:** This is NOT a UI feature. It is a core service.

```
src/services/context/
├── ContextEngine.ts
├── selector.ts
├── tokenizer.ts
├── summarizer.ts
├── securityScanner.ts
└── types.ts
```

**Responsibilities:**
- Gather information
- Rank sources
- Manage token budget
- Generate ContextBundle

---

## 13. Prompt Engine

```
src/services/prompt/
├── PromptBuilder.ts
├── templates.ts
├── formatter.ts
└── types.ts
```

**Responsibilities:**
- Generate System Prompt + Context + User Request

---

## 14. AI Provider Layer

```
src/services/providers/
├── Provider.ts
├── GroqProvider.ts
├── OpenRouterProvider.ts
├── ModelRouter.ts
└── types.ts
```

**Interface:**

```typescript
interface AIProvider {
  chat(messages: Message[]): Promise<Response>;
  stream(messages: Message[]): AsyncGenerator<string>;
  models(): Promise<Model[]>;
}
```

---

## 15. Storage Layer

```
src/services/database/
├── database.ts
├── migrations.ts
├── repositories/
│   ├── projectRepository.ts
│   ├── artifactRepository.ts
│   ├── taskRepository.ts
│   └── workflowRepository.ts
```

---

## 16. Zustand Stores

```
src/stores/
├── appStore.ts
├── settingsStore.ts
├── taskStore.ts
└── uiStore.ts
```

Use stores only for:
- Application state
- UI state

Not database data.

---

## 17. Tauri Backend Structure

```
src-tauri/
├── src/
│   ├── main.rs
│   ├── commands/
│   │   ├── database.rs
│   │   ├── filesystem.rs
│   │   └── secure_storage.rs
├── migrations/
└── tauri.conf.json
```

---

## 18. Workflow Storage

Built-in workflows:

```
workflows/
├── development/
│   ├── code-reviewer.json
│   ├── backend-engineer.json
├── security/
│   └── security-auditor.json
├── business/
│   └── product-manager.json
└── writing/
    └── technical-writer.json
```

---

## 19. Database Tables

v1:
- projects
- workflows
- tasks
- artifacts
- artifact_versions
- executions
- providers
- settings

---

## 20. Testing Structure

```
tests/
├── unit/
│   ├── context-engine.test.ts
│   ├── prompt-builder.test.ts
├── integration/
│   ├── task-execution.test.ts
└── fixtures/
```

---

## 21. Development Order

**Recommended implementation order:**

### Step 1
- Application shell
- Tauri
- React
- Routing
- Theme

### Step 2
- Storage foundation
- SQLite
- Repositories
- Settings

### Step 3
- Projects
- CRUD
- Imports
- Files

### Step 4
- Workflow system
- Schema
- Loader
- Browser

### Step 5
- Provider system
- Groq
- OpenRouter
- Streaming

### Step 6
- Context Engine
- Selection
- Token management

### Step 7
- Task Engine
- Execution pipeline
- Artifacts

### Step 8
- Polish
- UX
- Animations
- Export/import

---

## 22. Architecture Rule

When adding a feature, ask:

Does this belong to:
- Project?
- Workflow?
- Task?
- Artifact?
- Context?
- Provider?

If yes: Add it there.

Do not create random global utilities.

---

## 23. Final Structure Vision

The final application should naturally map:

```
features/
  Projects
  Workflows
  Tasks
  Artifacts

services/
  Context Engine
  Prompt Engine
  Provider Layer

database/
  Persistent Intelligence

Tauri/
  Native Capabilities
```

This structure allows Spire to grow from a personal AI tool into a complete personal AI operating environment without needing a rewrite.
"""

