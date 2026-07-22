# ============================================================
# 3. WORKFLOW-SCHEMA.md
# ============================================================
workflow_schema_content = """# Spire — AI Workflow Definition System

## Workflow Schema Specification

**Version:** 1.0  
**Status:** Final v1 Workflow Specification

---

## 1. Purpose

Workflows are the core intelligence units of Spire.

A Workflow represents:
- A professional role
- A methodology
- A problem-solving process
- Quality expectations
- Output standards

A Workflow is not simply a prompt. A prompt is generated from the workflow definition.

---

## 2. Core Concept

### Traditional AI:
```
User
 ↓
Prompt
 ↓
Answer
```

### Spire:
```
User Request
  +
Project Context
  +
Workflow Definition
  +
Model Capability
    ↓
Structured Artifact
```

---

## 3. Workflow Design Principles

### 3.1 Workflows Should Be Reusable
A good workflow should work across many projects.

**Example:** Security Auditor can analyze:
- Web applications
- APIs
- Embedded systems
- Infrastructure
- Mobile applications

### 3.2 Workflows Should Define Quality
The workflow must answer: "What makes a good result?"

**Examples:**
- A security audit should contain: severity rating, affected component, exploit explanation, remediation steps
- A marketing strategy should contain: target audience, positioning, channels, KPIs, timeline

### 3.3 Workflows Should Produce Deliverables
A workflow should create something useful.

**Examples:**
- Report
- Checklist
- Architecture document
- Roadmap
- Email
- Code review
- Specification

---

## 4. Workflow Object

```typescript
interface Workflow {
  id: string;
  name: string;
  version: string;
  category: string;
  icon: string;
  description: string;

  identity: WorkflowIdentity;
  capabilities: string[];
  methodology: WorkflowMethodology;
  qualityRules: string[];
  deliverables: DeliverableDefinition[];
  conversationStarters: string[];
  promptBlocks: PromptBlocks;
  modelPreferences: ModelPreferences;
  contextRequirements: ContextRequirements;
  futureExecution?: ExecutionConfiguration;

  createdAt: string;
  updatedAt: string;
}
```

---

## 5. Identity Block

Defines who the AI acts as.

**Example:**
```json
{
  "name": "Security Auditor",
  "identity": "You are a senior application security engineer specializing in threat modeling, vulnerability analysis, and secure software design."
}
```

Identity should define:
- Experience level
- Professional perspective
- Specialization
- Responsibility

---

## 6. Capabilities Block

Defines what the workflow can do.

**Example:**
```json
[
  "Perform OWASP security reviews",
  "Analyze authentication systems",
  "Identify architectural risks",
  "Recommend security improvements",
  "Create security reports"
]
```

Capabilities are not instructions. They describe expertise areas.

---

## 7. Methodology Block

Defines how the workflow thinks. This replaces simple prompts.

**Example:**
```json
{
  "steps": [
    "Understand system architecture",
    "Identify assets and trust boundaries",
    "Analyze threats",
    "Rank risks",
    "Recommend mitigations"
  ]
}
```

The methodology becomes the workflow's professional process.

---

## 8. Quality Rules

Quality rules define acceptance criteria.

**Example:**
```json
[
  "Every finding must include severity",
  "Recommendations must be actionable",
  "Explain impact clearly",
  "Separate facts from assumptions"
]
```

A workflow without quality rules is incomplete.

---

## 9. Deliverable Definitions

A workflow can create multiple output types.

**Example:**
```json
[
  {
    "type": "report",
    "name": "Security Assessment Report",
    "structure": [
      "Executive Summary",
      "Findings",
      "Risk Analysis",
      "Recommendations",
      "Conclusion"
    ]
  }
]
```

**Possible deliverables:**
```typescript
type DeliverableType =
  | "report"
  | "markdown"
  | "html"
  | "json"
  | "checklist"
  | "architecture"
  | "roadmap"
  | "email"
  | "code"
  | "presentation-outline";
```

---

## 10. Prompt Block System

The final prompt is generated from blocks.

**Example:**
```
SYSTEM
[Identity]
[Capabilities]
[Methodology]
[Quality Rules]
[Output Requirements]

CONTEXT
[Project Context]

TASK
[User Request]
```

---

## 11. Prompt Block Object

```typescript
interface PromptBlocks {
  identity: string;
  instructions: string;
  methodology: string;
  qualityRules: string;
  outputRules: string;
  communicationStyle: string;
}
```

---

## 12. Context Requirements

Workflows can specify what information they need.

**Example — Security Auditor:**
```json
{
  "required": [
    "sourceCode",
    "architecture",
    "dependencies",
    "configuration"
  ]
}
```

**Example — Architecture Reviewer:**
```json
{
  "required": [
    "projectDescription",
    "systemDesign",
    "technologyStack"
  ]
}
```

---

## 13. Model Preferences

Different workflows need different models.

**Example:**
```json
{
  "fast": "llama-3.1-70b",
  "reasoning": "claude-sonnet",
  "fallback": "gemini-flash"
}
```

The workflow recommends. The user decides.

---

## 14. Workflow Versioning

Workflows are versioned.

**Example:**
```
Security Auditor
  v1.0 — Initial workflow
  v1.1 — Added API security checks
  v2.0 — Changed methodology
```

Historical tasks always reference the workflow version used.

---

## 15. Conversation Starters

Workflows provide example actions.

**Example — Security Auditor:**
```json
[
  "Perform a security review of this project",
  "Check my API design for vulnerabilities",
  "Create a threat model"
]
```

**Example — Marketing Strategist:**
```json
[
  "Create a launch strategy",
  "Analyze competitors",
  "Develop a marketing roadmap"
]
```

---

## 16. Future Subagent Compatibility

v1 does NOT execute subagents. However, the schema supports future expansion.

**Future:**
```json
{
  "agents": [
    {
      "name": "Threat Modeler",
      "role": "Analyze attack surfaces"
    },
    {
      "name": "Dependency Scanner",
      "role": "Review libraries"
    }
  ]
}
```

**Future execution:**
```
Workflow
  ↓
Subagent A
  ↓
Subagent B
  ↓
Quality Reviewer
  ↓
Final Artifact
```

---

## 17. Example Workflow

### Production Readiness Auditor

```json
{
  "name": "Production Readiness Auditor",
  "category": "Operations",
  "description": "Evaluates whether a software system is ready for production deployment.",
  "identity": "You are a senior software reliability engineer responsible for evaluating production readiness.",
  "capabilities": [
    "Analyze architecture",
    "Review deployment practices",
    "Identify operational risks",
    "Evaluate monitoring"
  ],
  "methodology": [
    "Review architecture",
    "Evaluate reliability",
    "Check security",
    "Assess deployment",
    "Provide recommendations"
  ],
  "qualityRules": [
    "Provide severity ratings",
    "Explain business impact",
    "Give actionable fixes"
  ],
  "deliverables": [
    "Production Readiness Report",
    "Go/No-Go Checklist"
  ]
}
```

---

## 18. Built-In v1 Workflow Library

### Initial recommended library:

**Development**
- Senior Code Reviewer — Focus: maintainability, bugs, architecture, security
- Software Architect — Focus: system design, scalability, technology decisions
- Backend Engineer — Focus: APIs, databases, services

**Security**
- Security Auditor — Focus: OWASP, threat modeling, vulnerabilities

**Product**
- Product Manager — Focus: requirements, prioritization, roadmaps

**Writing**
- Technical Documentation Expert — Focus: manuals, architecture docs, developer documentation

**Operations**
- Production Readiness Auditor — Focus: deployment, reliability, monitoring

---

## 19. AI Workflow Generator (Future)

**Future feature:**

User: *"Create an expert for embedded Nordic nRF firmware development."*

Spire generates:
- Name
- Category
- Identity
- Capabilities
- Methodology
- Quality rules
- Deliverables
- Conversation starters
- Preferred models

The user reviews and saves.

---

## 20. Workflow Philosophy Summary

A Spire Workflow is:

```
Professional Identity
    +
Expertise
    +
Methodology
    +
Quality Standards
    +
Deliverables
    +
Context Requirements
    +
Model Strategy
    =
Reusable AI Capability
```

The workflow system is the foundation that allows Spire to become a personal AI workspace instead of another chat application.
"""

