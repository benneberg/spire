# ============================================================
# 4. PROMPT-ENGINEERING-STRATEGY.md
# ============================================================
prompt_engine_content = """# Spire — Prompt Engineering System

## Prompt Engineering Strategy Specification

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. Purpose

The Prompt Engine converts structured Spire objects into optimized AI requests.

The Prompt Engine is responsible for:
- Assembling workflow instructions
- Injecting project context
- Enforcing output requirements
- Managing token limits
- Creating reproducible executions
- Making prompts inspectable

The Prompt Engine is the bridge between:

```
Human Intent
  +
Workflow Intelligence
  +
Project Knowledge
  +
AI Model
```

---

## 2. Design Philosophy

Spire does not store giant manually written prompts.

Instead:

```
Workflow Definition
        ↓
Prompt Engine
        ↓
Generated Prompt
        ↓
AI Provider
```

The workflow is the source of truth. The generated prompt is an execution artifact.

---

## 3. Prompt Generation Pipeline

Every AI execution follows:

```
Task Created
  ↓
Load Workflow Version
  ↓
Build Context Bundle
  ↓
Select Model
  ↓
Generate System Prompt
  ↓
Generate User Prompt
  ↓
Validate Prompt
  ↓
Send To Provider
  ↓
Store Execution Trace
```

---

## 4. Prompt Components

The final AI request consists of:

```
SYSTEM MESSAGE
  +
CONTEXT SECTION
  +
TASK MESSAGE
  +
OUTPUT REQUIREMENTS
```

---

## 5. System Prompt Structure

The system prompt is generated from workflow blocks.

**Template:**

```
# Identity
{{identity}}

# Expertise
{{capabilities}}

# Methodology
{{methodology}}

# Quality Standards
{{qualityRules}}

# Communication Style
{{communicationStyle}}

# Output Expectations
{{outputRules}}
```

---

## 6. Context Injection

Context is never blindly appended.

The Context Engine prepares:

```
ContextBundle
  ↓
Prompt Engine
  ↓
Relevant Context
```

**Example:**

```
PROJECT CONTEXT

Project: Smart Home IoT Platform

Technology: ESP32, MQTT, React Dashboard

Relevant Files:
- src/device_manager.cpp
- src/api/routes.ts

Previous Artifact: Architecture Review v2
```

---

## 7. User Task Structure

The user's request becomes the task section.

**Template:**

```
# Task

Objective: {{userRequest}}

Deliverable: {{deliverableType}}

Additional Requirements: {{additionalInstructions}}
```

---

## 8. Complete Generated Prompt Example

**Example:**

```
SYSTEM:
You are a senior security engineer.

Your responsibilities:
- identify vulnerabilities
- analyze threats
- recommend mitigations

Your methodology:
1. Identify assets
2. Analyze attack surfaces
3. Evaluate risks

Quality requirements:
- Include severity ratings
- Explain impact
- Provide remediation

Output: Create a professional security report.

CONTEXT:
Project: API Gateway

Files: authentication.ts

TASK:
Perform a security audit.
```

---

## 9. Prompt Transparency

Every execution stores:

```typescript
interface PromptExecution {
  id: string;
  workflowVersion: string;
  systemPrompt: string;
  contextUsed: string;
  userPrompt: string;
  provider: string;
  model: string;
  createdAt: string;
}
```

The user can inspect:
- What was sent
- Why it was sent
- Which model answered
- Which context influenced the answer

---

## 10. Token Management

The Prompt Engine must operate within model limits.

**Priority order:**
1. User Request
2. Workflow Instructions
3. Current Project Summary
4. Selected Files
5. Previous Artifacts
6. Older History

When context is too large, the system reduces:
- Old conversations
- Old artifacts
- Large files

Before removing important instructions.

---

## 11. Context Compression Strategy

v1 uses deterministic compression.

**Example:**

Before:
- 50 previous messages
- 20 artifacts
- 500 files

After:
- Project Summary
- Relevant Files
- Latest Approved Artifacts
- Current Task

**Future:**
- Embeddings
- Semantic search
- Automatic retrieval

---

## 12. Model Routing

The Prompt Engine supports model selection.

**Example:**

Simple task (Technical explanation) → Fast model
Complex task (Architecture review) → Reasoning model

**Workflow recommendation:**

```typescript
interface ModelPreference {
  fast?: string;
  reasoning?: string;
  fallback?: string;
}
```

---

## 13. Revision Prompt Strategy

Artifacts are improved through controlled revision.

**Revision flow:**

```
Artifact v1
  +
User Feedback
  +
Workflow
    ↓
Revision Prompt
    ↓
Artifact v2
```

**Revision prompt:**

```
Previous Output: {{artifact}}

User Feedback: {{feedback}}

Task: Improve the artifact while preserving correct information.

Requirements: {{workflowQualityRules}}
```

---

## 14. Prompt Validation

Before execution, the Prompt Engine checks:

**Required sections — Must contain:**
- Identity
- Task
- Context
- Output requirements

**Safety checks — Prevent:**
- Empty workflows
- Missing instructions
- Oversized prompts
- Missing provider configuration

---

## 15. Prompt Templates

Spire supports reusable templates.

**Analysis Template**
Used by: auditors, reviewers, researchers

Structure:
1. Understand
2. Analyze
3. Identify Problems
4. Recommend Improvements
5. Summarize

**Creation Template**
Used by: writers, marketers, product managers

Structure:
1. Goal
2. Audience
3. Constraints
4. Create
5. Review
6. Improve

---

## 16. Structured Outputs

Where possible, workflows define structured responses.

**Example:**

```json
{
  "summary": "",
  "findings": [],
  "recommendations": []
}
```

**Benefits:**
- Easier rendering
- Better artifact management
- Future automation

---

## 17. Provider Adaptation

Different providers may require different formatting.

The Prompt Engine handles:
- OpenAI compatible APIs
- Anthropic style messages
- Local model formats

The workflow remains unchanged.

---

## 18. Debug Mode

Development mode exposes:

```
Workflow Loaded
  ↓
Context Selected
  ↓
Prompt Generated
  ↓
Provider Called
  ↓
Response Received
  ↓
Artifact Created
```

This makes improving workflows much easier.

---

## 19. Future Enhancements

Reserved for later phases:

### Automatic Prompt Optimization
AI evaluates:
- Clarity
- Missing requirements
- Ambiguity

### Prompt Testing
Run workflow against benchmark tasks.

### Workflow Evaluation
Measure:
- Quality
- Consistency
- Usefulness

---

## 20. Prompt Engine Summary

The Prompt Engine acts like a compiler:

```
Workflow Definition
        +
Project Context
        +
User Intent
        ↓
Generated AI Instruction
        ↓
High Quality Artifact
```

This separation allows Spire workflows to become increasingly sophisticated without creating unmaintainable prompt files.
"""

