# ============================================================
# 9. API_PROVIDER_SPEC.md
# ============================================================
api_provider_content = """# Spire — AI Provider Architecture

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. Purpose

The Provider Layer connects Spire workflows with external AI models.

Its responsibility:

> **Provide a unified interface for different AI services while keeping the rest of Spire provider-independent.**

---

## 2. Design Principle

The application should never know:
- Which company provides the model
- How authentication works
- How requests are formatted

The application only knows:

```
Send Messages
  ↓
Receive AI Response
```

---

## 3. Provider Architecture

```
             Spire Core
                 |
         Provider Interface
                 |
     --------------------------------
     |              |              |
   Groq        OpenRouter      Future
                              OpenAI
                              Anthropic
                              Gemini
```

---

## 4. Provider Interface

Every provider implements:

```typescript
interface AIProvider {
  id: string;
  name: string;

  chat(request: ChatRequest): Promise<ChatResponse>;

  stream(request: ChatRequest): AsyncGenerator<string>;

  getModels(): Promise<ModelInfo[]>;

  validateConnection(): Promise<boolean>;
}
```

---

## 5. Chat Request

```typescript
interface ChatRequest {
  messages: Message[];
  model: string;
  temperature: number;
  maxTokens: number;
  stream: boolean;
}
```

---

## 6. Message Format

Spire uses OpenAI-compatible messages internally.

```typescript
interface Message {
  role: "system" | "user" | "assistant";
  content: string;
}
```

This allows easy provider switching.

---

## 7. Supported v1 Providers

### 7.1 Groq

**Purpose:** Fast execution.

**Best for:**
- Simple analysis
- Documentation
- Quick iterations
- Everyday tasks

**Examples:** Llama models, other available Groq-hosted models

**Configuration:**
```json
{
  "provider": "groq",
  "apiKey": "encrypted",
  "defaultModel": "selected-model"
}
```

### 7.2 OpenRouter

**Purpose:** Model flexibility.

**Best for:**
- Complex reasoning
- Architecture
- Security audits
- Strategic planning

**Supports access to:**
- Anthropic models
- OpenAI models
- Google models
- Open-source models

**Configuration:**
```json
{
  "provider": "openrouter",
  "apiKey": "encrypted",
  "defaultModel": "selected-model"
}
```

---

## 8. Provider Storage Model

```typescript
interface ProviderConfig {
  id: string;
  type: string;
  name: string;
  encryptedApiKey: string;
  enabled: boolean;
  defaultModel: string;
  settings: ProviderSettings;
}
```

---

## 9. API Key Security

Keys are sensitive.

### Rules

**Never:**
- Store plain text
- Include in exports
- Send to AI models

**Storage:**
```
User Key
  ↓
Encryption
  ↓
Secure Local Storage
  ↓
Provider Request
```

**Tauri:**
- Preferred: OS keychain integration
- Fallback: Encrypted SQLite storage

---

## 10. Model Registry

Spire maintains model information.

```typescript
interface ModelInfo {
  id: string;
  provider: string;
  name: string;
  contextWindow: number;
  supportsVision: boolean;
  supportsStreaming: boolean;
  capabilities: string[];
}
```

**Example:**
```json
{
  "id": "model-name",
  "provider": "openrouter",
  "contextWindow": 200000,
  "supportsStreaming": true,
  "capabilities": [
    "reasoning",
    "coding",
    "analysis"
  ]
}
```

---

## 11. Model Capability System

Models should not only have names. They should have capabilities.

**Example:**

| Capability | Model |
|-----------|-------|
| Fast | Groq Llama |
| Reasoning | Claude Sonnet |
| Coding | Specialized Code Model |
| Vision | Multimodal Model |

---

## 12. Workflow Model Preferences

Workflows can specify preferred models.

**Example:**
```json
{
  "name": "Security Auditor",
  "modelPreferences": {
    "primary": "reasoning",
    "fallback": "fast"
  }
}
```

**Meaning:**
```
Use: Reasoning model first
  ↓
Fast model if unavailable
```

---

## 13. Model Router

The Model Router decides:

```
Task
  ↓
Workflow Requirements
  ↓
Available Providers
  ↓
Best Model
```

**Interface:**
```typescript
interface ModelRouter {
  selectModel(workflow: Workflow, task: Task): Promise<ModelSelection>;
}
```

---

## 14. Routing Logic v1

Simple rules.

**Priority:**
1. User override
2. Workflow preference
3. Capability match
4. Available model
5. Default provider

**Example:**

```
Security Audit:
  Need: reasoning
  Available: Claude ✓, Llama ✓
  Selected: Claude
```

---

## 15. Streaming Architecture

**Flow:**

```
User Starts Task
  ↓
Task Engine
  ↓
Provider
  ↓
Streaming Tokens
  ↓
UI Updates
  ↓
Artifact Generated
```

Frontend receives: `AsyncGenerator<string>`

---

## 16. Error Handling

### Provider errors:

**Authentication**
- Invalid API Key
- Action: Open Provider Settings

**Rate Limit**
- Provider limit reached
- Action: Try fallback model

**Timeout**
- Action: Retry or Switch provider

---

## 17. Usage Tracking

Each execution stores:

```typescript
interface UsageRecord {
  provider: string;
  model: string;
  inputTokens: number;
  outputTokens: number;
  duration: number;
  estimatedCost: number;
}
```

**Purpose:**
- Understand usage
- Compare models
- Optimize workflows

---

## 18. Export Rules

Workspace exports include:

**YES:**
- Provider names
- Model preferences
- Workflow settings

**NO:**
- API keys
- Authentication tokens

---

## 19. Future Providers

Architecture supports:

### OpenAI
- Use cases: General intelligence, structured outputs

### Anthropic
- Use cases: Reasoning, long documents

### Google Gemini
- Use cases: Multimodal tasks

### Ollama
- Use cases: Local privacy, offline mode

### LM Studio
- Use cases: Local development models

---

## 20. GitHub Authentication Preparation

Future GitHub integration requires separate authentication. Not an AI provider.

**Storage:**
```typescript
interface GitHubConfig {
  enabled: boolean;
  encryptedToken: string;
  permissions: string[];
}
```

**Recommended permissions:**

v1/v2: Read only
- `repo:read`
- `contents:read`

The GitHub token should only allow:
- Repository listing
- File reading
- Commit history reading

**Never:**
- Push
- Delete
- Modify

Unless explicitly enabled later.

---

## 21. Provider Development Pattern

Adding a new provider:

```
Create: providers/NewProvider.ts
  ↓
Implement: AIProvider
  ↓
Register: ProviderRegistry
  ↓
Add tests
```

No changes required elsewhere.

---

## 22. Provider Registry

```typescript
interface ProviderRegistry {
  register(provider: AIProvider): void;
  get(id: string): AIProvider;
}
```

---

## 23. Provider Layer Summary

The Provider Layer gives Spire:

```
One Workspace
  ↓
Many Intelligence Sources
  ↓
Optimal Model Selection
  ↓
Better Results
  ↓
No Vendor Lock-in
```

The AI model is replaceable.

The valuable part is:
- Projects
- Workflows
- Context
- Artifacts
- Knowledge
"""

