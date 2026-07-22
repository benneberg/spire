# ============================================================
# 6. TASK_EXECUTION_ENGINE.md
# ============================================================
task_execution_content = """# Spire — Task Execution Engine

## Task Execution Engine Specification

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. Purpose

The Task Execution Engine manages the complete lifecycle of AI-powered work in Spire.

It coordinates:
- Workflow loading
- Context preparation
- Prompt generation
- Provider communication
- Streaming responses
- Artifact creation
- User review
- Revision

---

## 2. Core Philosophy

A Task is not a conversation.

A Task is: **A controlled attempt to transform a user objective into a reusable artifact.**

### Traditional AI:
```
Question
 ↓
Answer
```

### Spire:
```
Objective
  ↓
Workflow
  ↓
Context
  ↓
Execution
  ↓
Artifact
  ↓
Knowledge
```

---

## 3. Task Lifecycle

A task moves through defined states.

```
DRAFT
  ↓
PREPARING
  ↓
RUNNING
  ↓
REVIEW
  ↓
COMPLETED

or

FAILED
```

---

## 4. Task States

```typescript
type TaskStatus =
  | "draft"
  | "preparing"
  | "running"
  | "review"
  | "completed"
  | "failed"
  | "cancelled";
```

---

## 5. Task Creation Flow

User creates a task.

**Required:**
- Project + Workflow + User Request + Deliverable Type

**Optional:**
- Selected Files
- Additional Instructions
- Model Override
- Previous Artifact Reference

**Example:**

```
Project: Smart Home Platform
Workflow: Security Auditor
Request: Analyze authentication security.
Deliverable: Security Report
```

---

## 6. Execution Pipeline

The Task Engine executes:

```
1. Validate Task
  ↓
2. Load Workflow Version
  ↓
3. Build Context Bundle
  ↓
4. Generate Prompt
  ↓
5. Select AI Provider
  ↓
6. Execute AI Request
  ↓
7. Stream Response
  ↓
8. Create Draft Artifact
  ↓
9. User Review
  ↓
10. Save Final Artifact
```

---

## 7. Task Preparation

Before execution, the system validates:

**Workflow**
- Required: identity, instructions, quality rules, output format

**Project**
- Required: valid project reference

**Provider**
- Required: available API key, selected model

---

## 8. Execution Context

Every execution receives:

```typescript
interface ExecutionContext {
  taskId: string;
  workflowId: string;
  workflowVersion: string;
  projectId: string;
  contextBundleId: string;
  model: string;
  provider: string;
}
```

---

## 9. Provider Execution

The engine calls the provider abstraction.

```typescript
interface TaskRunner {
  execute(task: Task): Promise<TaskResult>;
  stream(task: Task): AsyncGenerator<string>;
}
```

---

## 10. Streaming Responses

The UI should receive incremental output.

**Example:**

```
Analyzing project...
  ↓
Identifying authentication flow...
  ↓
Generating findings...
  ↓
Creating report...
```

**Benefits:**
- Better UX
- Perceived speed
- Easier cancellation

---

## 11. Execution Logging

Every run creates an execution record.

```typescript
interface ExecutionRecord {
  id: string;
  taskId: string;
  provider: string;
  model: string;
  startedAt: string;
  completedAt: string;
  duration: number;
  tokenUsage?: TokenUsage;
  promptId: string;
  status: string;
}
```

---

## 12. Human Review Gate

v1 requires human approval.

After generation:

```
AI Draft
  ↓
User Review
  ↓
Approve
  or
Request Changes
  ↓
New Version
```

The AI does not automatically publish final outputs.

---

## 13. Artifact Creation

A successful execution creates an Artifact.

**Example:**

```
Task: Create architecture document
Produces:
Artifact: Architecture Overview.md
Version: 1
```

Artifact metadata stores:

```typescript
interface ArtifactOrigin {
  taskId: string;
  workflowId: string;
  workflowVersion: string;
  model: string;
  createdAt: string;
}
```

---

## 14. Revision Flow

A revision is a new execution.

**Example:**

```
Artifact v1
  ↓
User: "Make this more suitable for investors"
  ↓
Revision Task
  ↓
Artifact v2
```

Never overwrite previous versions.

---

## 15. Failure Handling

### Possible failures:

**Provider Failure**
- Examples: timeout, unavailable model, rate limit
- Response: Retry, Change Model, Cancel

**Context Failure**
- Examples: too much data, missing required information
- Response: Adjust Context, Remove Sources, Continue

**Generation Failure**
- Examples: invalid output, incomplete response
- Response: Retry, Modify Instructions, Cancel

---

## 16. Cancellation

Long tasks can be cancelled.

**Example:**

```
RUNNING
  ↓
CANCEL REQUEST
  ↓
STOP STREAM
  ↓
SAVE PARTIAL RESULT
```

Partial outputs may optionally become drafts.

---

## 17. Deliverable Handling

The execution engine supports different output types.

**Examples:**

| Type | Handling |
|------|----------|
| Markdown | Saved directly |
| JSON | Validated before storage |
| HTML | Stored as artifact content |
| Code | Stored with language metadata |

---

## 18. Structured Output Validation

Future-ready.

**Example:**

Workflow requires:
```json
{
  "summary": "",
  "issues": [],
  "recommendations": []
}
```

Engine can validate:
- Valid JSON?
- Required fields present?
- Correct format?

---

## 19. Execution History

Users can view:

```
Task History
--------------------------------
Security Audit

Created: July 22 2026
Workflow: Security Auditor v1
Model: Claude Sonnet
Result: Completed
Artifact: Security Report v3
```

---

## 20. Task Service Interface

```typescript
interface TaskService {
  createTask(input: CreateTaskInput): Promise<Task>;

  runTask(taskId: string): Promise<TaskResult>;

  reviseArtifact(artifactId: string, feedback: string): Promise<Task>;

  getHistory(projectId: string): Promise<Task[]>;
}
```

---

## 21. Future Extensions

The architecture supports:

### Multi-Step Workflows

**Example:**
```
Research
  ↓
Analysis
  ↓
Review
  ↓
Formatting
```

### Agent Teams

**Example:**
```
Security Workflow
  ↓
Threat Modeler
  ↓
Code Reviewer
  ↓
Compliance Analyst
  ↓
Final Auditor
```

### Automated Tasks

**Future:**
```
Every Monday:
- Analyze project health
- Generate report
- Notify user
```

---

## 22. Task Execution Summary

The Task Engine transforms Spire from:

> **AI Chat Application**

into:

> **Personal AI Production System**

```
Input
  ↓
Process
  ↓
Review
  ↓
Artifact
  ↓
Knowledge
```

Every task becomes a durable piece of intelligence inside the workspace.
"""

