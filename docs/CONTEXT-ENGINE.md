# ============================================================
# 5. CONTEXT-ENGINE.md
# ============================================================
context_engine_content = """# Spire — Context Engine

## Context Engine Specification

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. Purpose

The Context Engine transforms raw workspace information into a focused, relevant context package for AI execution.

Its responsibility:

> **Give the AI the right information, in the right order, at the right time.**

Without a Context Engine, Spire becomes another chat interface.

With a Context Engine, Spire becomes a project-aware AI workspace.

---

## 2. Core Concept

The AI should not receive everything.

The AI should receive:

```
Project Understanding
  +
Relevant Sources
  +
Previous Knowledge
  +
Current Objective
```

---

## 3. Context Pipeline

Every task execution follows:

```
Task Created
  ↓
Context Requirements Loaded
  ↓
Project Information Collected
  ↓
Relevant Sources Selected
  ↓
Context Budget Applied
  ↓
Context Bundle Generated
  ↓
Prompt Engine Receives Bundle
```

---

## 4. Context Bundle

The Context Engine produces a standardized object.

```typescript
interface ContextBundle {
  id: string;
  projectSummary: string;
  projectMetadata: ProjectContext;
  selectedSources: ContextSource[];
  relatedArtifacts: ArtifactReference[];
  previousDecisions: string[];
  tokenEstimate: number;
  createdAt: string;
}
```

---

## 5. Context Sources

A context source represents information provided to the AI.

```typescript
interface ContextSource {
  id: string;
  type: "file" | "document" | "code" | "url" | "note" | "artifact" | "conversation";
  title: string;
  content: string;
  priority: number;
  relevanceScore?: number;
}
```

---

## 6. Context Priority System

Not all information has equal importance.

**Priority order:**
1. Current user request
2. Workflow requirements
3. Project summary
4. Selected user files
5. Recent approved artifacts
6. Project notes
7. Historical conversations
8. Older information

---

## 7. Project Understanding Layer

Every project should develop a compact identity.

**Example:**

```
Project: Smart Home Controller

Purpose: IoT platform controlling sensors and devices.

Technology: ESP32, MQTT, React, Node.js

Architecture: Embedded devices communicate with backend services.
```

This summary becomes the foundation for future tasks.

---

## 8. Project Summary Generation

v1 supports generated summaries.

**Process:**

```
New Project
  ↓
User Adds Information
  ↓
Generate Project Summary
  ↓
Store Summary
  ↓
Reuse In Future Tasks
```

**Example:**

Initial input:
- 50 source files
- README
- package.json
- Hardware notes

Result:

```
Project Intelligence Summary
```

---

## 9. Source Selection

v1 uses deterministic selection.

### Selection Methods

**Manual Selection**
User chooses: files, artifacts, documents

**Workflow Requirements**
Workflow defines needed information.

**Example:** Security Auditor requires:
- Source code
- Dependencies
- Architecture
- Authentication information

**Keyword Matching**
Simple relevance scoring:

**Example:**
- **Task:** "Review authentication security"
- **Relevant:** auth.ts, login.service.ts, jwt.config.ts
- **Less relevant:** homepage.css, logo.svg

---

## 10. Context Requirements

Workflows declare requirements.

**Example:**

```json
{
  "name": "Code Reviewer",
  "contextRequirements": [
    "sourceCode",
    "architecture",
    "tests",
    "dependencies"
  ]
}
```

The Context Engine uses this to prepare information.

---

## 11. Token Budget Management

The Context Engine protects model limits.

**Example budget:**

| Component | Allocation |
|-----------|-----------|
| System instructions | 20% |
| Project summary | 20% |
| Relevant sources | 45% |
| User request | 15% |

When the budget is exceeded, reduce:
- Old conversations
- Old artifacts
- Large files

Never reduce:
- Workflow instructions
- Current task
- Essential project information

---

## 12. Large File Handling

Large files should not always be injected completely.

**Example:** A 20,000 line file.

Instead:
```
File Overview
  +
Relevant Sections
  +
User Requested Area
```

**Future:**
- Syntax-aware parsing
- AST analysis
- Embeddings

---

## 13. Artifact Memory

Artifacts become project knowledge.

**Example:**

```
Project: My SaaS Application

Artifacts:
- Architecture Document v2
- Security Review v1
- Database Design v3
- API Specification v1
```

Future tasks can use these as trusted references.

---

## 14. Context Snapshot

Every task stores the exact context used.

**Purpose:**
- Reproducibility
- Debugging
- Comparison
- Auditing

**Example:**

```
Task #42
Created: July 22 2026

Used:
- Architecture.md v2
- Backend files
- Project summary v3
- Workflow: Senior Architect v1.1
```

---

## 15. Context Preview UI

Before execution, users should see:

```
AI will receive:
✓ Project Summary
✓ package.json
✓ Architecture Document
✓ API Notes

Excluded:
○ Old Chat History
○ Temporary Files
```

The user remains in control.

---

## 16. Context Security

Sensitive information handling:

**Potentially sensitive:**
- API keys
- Passwords
- Certificates
- Secrets

The Context Engine should detect obvious patterns:

**Examples:**
- `API_KEY=`
- `PASSWORD=`
- `PRIVATE_KEY`
- `TOKEN=`

**Behavior:**

Warn user:

> Possible secret detected. Send to AI provider?
> [Cancel] [Include]

---

## 17. Future Knowledge Layer

The v1 architecture prepares for:

### Knowledge Packs

**Examples:**
- **Security:** OWASP, CWE, NIST, CIS
- **Accessibility:** WCAG, ARIA, Apple HIG
- **Marketing:** SEO principles, Marketing frameworks, Brand guidelines

### Semantic Retrieval

**Future:**
```
Project Files
  ↓
Embeddings
  ↓
Vector Search
  ↓
Relevant Context
```

---

## 18. Future Project Intelligence

**Long-term goal:**

Spire automatically understands:
- Architecture
- Technology Stack
- Dependencies
- Patterns
- Risks
- Technical Debt
- History

---

## 19. Context Engine Service Interface

```typescript
interface ContextEngine {
  buildContext(task: Task): Promise<ContextBundle>;

  estimateTokens(context: ContextBundle): number;

  summarize(content: string): Promise<string>;
}
```

---

## 20. Context Engine Summary

The Context Engine is the memory bridge:

```
Raw Information
  ↓
Understanding
  ↓
Relevant Context
  ↓
AI Reasoning
  ↓
Artifact
  ↓
New Knowledge
```

It is the mechanism that allows Spire to become more valuable the longer it is used.
"""

