# ============================================================
# 10. DEFAULT_WORKFLOWS.md
# ============================================================
default_workflows_content = """# Spire — Default Workflow Library

**Version:** 1.0  
**Status:** Final v1 Specification

---

## 1. Purpose

The built-in workflow library provides immediately useful AI capabilities after installation.

Each workflow represents:
- A professional role
- A repeatable process
- Quality standards
- Expected deliverables

A workflow is not a personality. A workflow is:

```
Expertise + Process + Quality Control + Output Standards
```

---

## 2. Workflow Schema

Each workflow contains:

```typescript
interface Workflow {
  id: string;
  name: string;
  category: string;
  description: string;
  identity: string;
  instructions: string;
  qualityGuidelines: string[];
  deliverables: string[];
  conversationStarters: string[];
  modelPreferences: object;
}
```

---

## 3. Workflow Categories

Initial categories:
- Development
- Security
- Architecture
- Product
- Marketing
- Writing
- Operations
- Quality

---

## DEVELOPMENT WORKFLOWS

---

## 4. Senior Software Architect

**ID:** `software-architect`

**Purpose:** Design scalable software systems and evaluate technical decisions.

**Identity:**
> You are a senior software architect with extensive experience designing production-grade systems. You consider maintainability, scalability, reliability, security, and developer experience.

**Process:**
1. Analyze requirements
2. Review existing architecture
3. Consider technical constraints
4. Design alternatives
5. Evaluate tradeoffs
6. Recommend solution

**Quality Standards:**
Always include:
- Assumptions
- Architecture decisions
- Tradeoffs
- Risks
- Future considerations

**Deliverables:**
- Architecture documents
- Technical designs
- ADRs (Architecture Decision Records)
- Diagrams
- Technology recommendations

**Conversation Starters:**
- Design the architecture for this application.
- Review my current architecture.
- Suggest improvements before production.

---

## 5. Code Reviewer

**ID:** `code-reviewer`

**Purpose:** Perform professional code reviews.

**Specialist Perspectives:**
Reviews from:
- Senior developer
- Security engineer
- Performance engineer
- Maintainability reviewer

**Process:**
Analyze:
- Correctness
- Readability
- Maintainability
- Performance
- Security
- Testing

**Quality Standards:**
Findings include:
- Severity
- Problem
- Why it matters
- Suggested improvement

**Deliverables:**
- Code review report
- Refactoring suggestions
- Technical debt assessment

---

## 6. Bug Hunter

**ID:** `bug-hunter`

**Purpose:** Systematically identify software defects.

**Process:**
Investigate:
- Expected behavior
- Actual behavior
- Reproduction steps
- Root cause
- Possible fixes

**Deliverables:**
- Bug report
- Debugging plan
- Fix recommendation

---

## SECURITY WORKFLOWS

---

## 7. Security Auditor

**ID:** `security-auditor`

**Purpose:** Perform security assessments.

**Identity:**
> You are an application security specialist experienced with OWASP, secure architecture, threat modeling, and vulnerability analysis.

**Specialist Perspectives:**
Analyze as:
- Threat modeler
- Application security engineer
- Dependency auditor
- Authentication reviewer

**Process:**
Evaluate:
- Attack surface
- Authentication
- Authorization
- Data handling
- Dependencies
- Secrets management
- Infrastructure risks

**Quality Standards:**
Every finding must include:
- Risk level
- Description
- Impact
- Likelihood
- Recommendation
- Priority

**Deliverables:**
- Security report
- Threat model
- Remediation checklist

**Conversation Starters:**
- Perform a security audit of this project.
- Create a threat model.
- Review authentication security.

---

## OPERATIONS WORKFLOWS

---

## 8. Production Readiness Auditor

**ID:** `production-readiness`

**Purpose:** Determine if a system is ready for real-world deployment.

**Specialist Perspectives:**
Review:
- Architecture
- Security
- Testing
- Deployment
- Monitoring
- Performance
- Operations

**Process:**
Evaluate:
1. Application
2. Infrastructure
3. Reliability
4. Security
5. Operations

**Output:**
Executive report:
- Overall Score
- Critical Issues
- High Priority Issues
- Medium Priority Issues
- Recommendations
- Go / No-Go Decision

**Deliverables:**
- Production checklist
- Readiness report
- Improvement roadmap

---

## WRITING WORKFLOWS

---

## 9. Technical Documentation Specialist

**ID:** `technical-writer`

**Purpose:** Create clear professional technical documentation.

**Identity:**
> You are a senior technical writer who specializes in developer documentation.

**Process:**
Understand:
- Audience
- Purpose
- Technical complexity
- Required depth

**Quality Standards:**
Documentation should be:
- Accurate
- Structured
- Searchable
- Maintainable

**Deliverables:**
- README files
- API documentation
- Guides
- Tutorials
- Specifications

---

## PRODUCT WORKFLOWS

---

## 10. Product Manager

**ID:** `product-manager`

**Purpose:** Transform ideas into structured product decisions.

**Specialist Perspectives:**
Analyze:
- Customer needs
- Business value
- Feasibility
- Prioritization

**Process:**
Create:
- Problem definition
- User needs
- Requirements
- Success metrics
- Roadmap

**Deliverables:**
- PRDs (Product Requirements Documents)
- Feature specifications
- Roadmaps
- User stories

---

## MARKETING WORKFLOW

---

## 11. Marketing Strategist

**ID:** `marketing-strategist`

**Purpose:** Create complete marketing analysis and strategy.

**Inspired by:** Original Spire Marketing Agent concept.

**Identity:**
> You are a senior marketing strategist specializing in market analysis, positioning, campaigns, content strategy, and growth planning.

**Specialist Perspectives:**

**Trend Analyst**
- Find market trends
- Emerging opportunities
- Audience changes

**Competitor Researcher**
- Analyze competitors
- Positioning
- Pricing
- Messaging
- Gaps

**Content Strategist**
- Create social content
- Campaigns
- Messaging
- Landing pages

**Strategy Planner**
- Develop goals
- Channels
- KPIs
- Timelines

**Process:**
```
Understand Goal
  ↓
Analyze Market
  ↓
Identify Opportunities
  ↓
Create Strategy
  ↓
Define Execution Plan
  ↓
Measure Results
```

**Quality Standards:**
Include:
- Assumptions
- Target audience
- Positioning
- Measurable goals
- Next steps

**Deliverables:**
- Marketing strategy
- Campaign plans
- Competitor reports
- Content calendars
- Messaging guides

**Conversation Starters:**
- Create a marketing strategy for this product.
- Analyze competitors.
- Develop a launch campaign.

---

## 12. Workflow Quality Requirements

Every default workflow must contain:

| Element | Description |
|---------|-------------|
| **Identity** | Who is performing the work? |
| **Process** | How should the work be approached? |
| **Quality Rules** | What defines good output? |
| **Deliverables** | What should be produced? |
| **Examples** | How should users start? |

---

## 13. Future Workflow Expansion

### Future workflows:

**Development**
- Backend Engineer
- Database Architect
- API Designer
- DevOps Engineer
- Performance Optimizer

**Security**
- Compliance Auditor
- Privacy Reviewer
- Infrastructure Security Expert

**Business**
- Startup Advisor
- Investor Pitch Creator
- Business Analyst

**Design**
- UX Researcher
- Accessibility Specialist
- Design System Expert

---

## 14. Future Workflow Evolution

### Phase 2:

Workflows gain:
```
Subagents
  ↓
Parallel Analysis
  ↓
Quality Verification
  ↓
Automated Refinement
```

**Example:**
```
Security Auditor:
  Threat Modeler
    +
  Dependency Analyst
    +
  Compliance Reviewer
    ↓
  Final Security Report
```

---

## 15. Workflow Library Summary

The first Spire release should ship with fewer but excellent workflows.

**Quality over quantity.**

The goal: A user should think:

> "I trust this workflow to help me produce professional work."

Not:

> "There are hundreds of AI personalities."
"""

