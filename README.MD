# 🔄 AI Feature Migration Workflow

[English](./README.md) | [中文](./README.zh-CN.md)

> A human-reviewed AI-assisted workflow for semantic feature migration across different software projects.

This project provides a practical workflow for migrating features between projects while preserving architecture boundaries, platform-specific implementations, and target-system conventions.

---

# 📌 Problem Statement

Traditional copy-paste migration or AI-generated migration often fails because:

- Source and target projects have different architectures
- AI lacks full context of both systems
- Infrastructure dependencies differ
- Utility classes and frameworks are inconsistent
- Platform-specific logic gets broken
- Hidden coupling is difficult to identify

Common failures include:

- Missing dependencies
- Incorrect framework adaptation
- API incompatibilities
- Runtime regressions
- Broken DI / Bean injection
- Incorrect infrastructure assumptions

This workflow solves those problems using:

- Dual-project AI collaboration
- Human relay verification
- Semantic dependency analysis
- Compatibility validation
- Architecture-aware adaptation

---

# 🎯 Core Philosophy

```text
AI does not fully understand both projects simultaneously.

Instead:
- Source Project AI understands business intent
- Target Project AI understands target architecture
- Human acts as the context bridge
```

This creates a safer migration workflow:

```text
Human-in-the-loop semantic feature migration
```

---

# 🏗️ Architecture

```text
Source Project AI
    ↓
Feature & Dependency Analysis
    ↓
Human Relay
    ↓
Target Project AI
    ↓
Capability Verification
    ↓
Human Relay
    ↓
Source AI Refines Migration Plan
    ↓
Target AI Executes Adaptation
    ↓
Compile & Test
    ↓
Audit & Validation
```

---

# ✅ Use Cases

This workflow is useful for:

- Legacy → New system migration
- Monolith → Microservice migration
- Android → HarmonyOS migration
- Java → Kotlin migration
- SaaS → Private deployment migration
- Cross-project feature reuse
- OEM customer customization
- Shared business capability extraction

---

# ❌ When NOT to Use This

Do NOT use this workflow for:

- Simple utility copying
- Small isolated functions
- Standard git merge scenarios
- Pure frontend component reuse
- Projects with identical architecture

In those cases, direct migration is usually enough.

---

# 🚀 Standard Workflow

---

# Step 1 — Source Project Analysis

## Goal

Analyze the source feature and identify:

- Core business logic
- Dependency chain
- Required utilities
- Infrastructure coupling
- Migration risks
- Required target capabilities

---

## Prompt Example

```text
I want to migrate the XXXXX feature.

Core files:
- XXXService.java
- XXXManager.java
- XXXController.java

Please analyze:
1. Feature migration considerations
2. Migration strategy
3. Required files
4. Utility classes and helper methods
5. Infrastructure dependencies
6. What needs to be verified in the target project

Ask me questions where target-project confirmation is required.
```

---

# Step 2 — Target Project Verification

## Goal

Verify whether the target project contains:

- Equivalent utilities
- Matching infrastructure
- Compatible frameworks
- Alternative implementations
- Required architecture support

---

## Prompt Example

```text
I want to migrate the XXXXX feature into this project.

The source-project analysis requires confirmation for:

- Redis utility support
- MQ producer implementation
- UserContext helper
- Permission framework
- Transaction wrapper

Please verify:
1. Whether these capabilities exist
2. What alternatives should be used
3. Any architectural differences
4. Any migration risks
```

---

# Step 3 — Migration Plan Refinement

## Goal

Feed the target-project answers back into the source-project AI.

This allows the source AI to:

- Refine the migration plan
- Remove incorrect assumptions
- Adapt to target architecture
- Generate a safer migration strategy

---

## Prompt Example

```text
Here are the target-project confirmations:

- Redis → Spring Cache
- MQ → RocketMQ
- No UserContext helper
- Permission framework differs

Please generate:
1. Final migration plan
2. Required file mapping
3. Replacement strategy
4. Risk analysis
5. Adaptation recommendations
```

---

# Step 4 — Target-side Adaptation

## Goal

Let the target-project AI perform localized adaptation.

This is NOT direct copying.

The target AI should:

- Adapt coding style
- Adapt architecture
- Replace incompatible infrastructure
- Preserve target conventions
- Integrate with existing patterns

---

## Prompt Example

```text
Please migrate the XXXXX feature into the target project.

Migration plan:
[paste migration plan]

Target file locations:
[paste approximate locations]

Requirements:
1. Adapt to target architecture
2. Preserve target conventions
3. Replace incompatible dependencies
4. Avoid direct copy-paste migration
```

---

# Step 5 — Compile & Test

## Goal

Create a rapid feedback loop.

Detect:

- Missing dependencies
- DI failures
- Compilation errors
- Incorrect API assumptions
- Runtime incompatibilities

---

## Recommended Commands

```bash
mvn test
```

or:

```bash
gradle test
```

---

# Step 6 — Migration Audit

## Goal

Prevent hidden regressions and AI hallucinations.

Audit:

- Core business methods
- Conditional logic
- Permission checks
- Transaction boundaries
- Cache behavior
- MQ behavior
- Error handling
- Fallback logic

---

## Prompt Example

```text
Please compare the migrated implementation with the source implementation.

Focus on:
1. Business logic consistency
2. Conditional branches
3. Error handling
4. Transaction behavior
5. Cache/MQ differences
6. Missing edge cases
```

---

# 🛡️ Migration Boundary Rules

Always define:

## What SHOULD be migrated

Examples:

- Business logic
- Validation rules
- Calculation logic
- Core workflows

---

## What SHOULD NOT be migrated

Examples:

- UI implementation
- Infrastructure layer
- ORM implementation
- MQ implementation
- Cache implementation
- Authentication framework
- Platform-specific code

---

# 📑 Dependency Classification

Recommended AI output structure:

| Dependency Type | Example | Action |
|---|---|---|
| Required Dependency | UserService | Must migrate |
| Replaceable Utility | RedisUtil | Replace |
| Platform Component | Android Context | Skip |
| Infrastructure Coupling | Kafka | Adapt |
| Optional Feature | Metrics | Optional |

---

# 📊 Compatibility Matrix

Example:

| Capability | Source | Target | Action |
|---|---|---|---|
| Cache | Redisson | Spring Cache | Replace |
| MQ | Kafka | RocketMQ | Adapt |
| ORM | MyBatis | JPA | Rewrite |
| Auth | JWT | OAuth2 | Manual |

---

# ⚠️ Migration Risk Levels

| Level | Meaning |
|---|---|
| Low | Pure business logic |
| Medium | Utility replacement required |
| High | Infrastructure coupling exists |
| Critical | Platform/runtime differences |

---

# ❌ Common AI Failure Cases

---

## Case 1 — AI Assumes Missing Dependencies Exist

### Problem

AI hallucinated utility classes.

### Prevention

Always verify target-project capabilities first.

---

## Case 2 — Direct Copy-Paste Migration

### Problem

AI copied source architecture directly.

### Risk

- Architecture inconsistency
- Technical debt
- Runtime issues

### Prevention

Force target-side adaptation.

---

## Case 3 — Hidden Infrastructure Coupling

### Problem

Feature silently depends on:

- MQ
- cache
- distributed transactions
- ThreadLocal
- lifecycle hooks

### Prevention

Perform dependency classification.

---

## Case 4 — Incorrect Framework Adaptation

### Problem

AI incorrectly maps:

- ORM
- auth
- DI
- async execution

### Prevention

Use compatibility verification before migration.

---

# 📂 Recommended Repository Structure

```text
ai-feature-migration-workflow/
│
├── README.md
├── README.zh-CN.md
│
├── PROMPTS/
│   ├── source-analysis.md
│   ├── target-verification.md
│   ├── migration-planning.md
│   ├── target-adaptation.md
│   └── fix-test-errors.md
│
├── docs/
│   ├── architecture.md
│   ├── migration-risks.md
│   ├── compatibility-matrix.md
│   └── best-practices.md
│
├── templates/
│   ├── dependency-checklist.md
│   ├── migration-plan.md
│   ├── compatibility-report.md
│   └── risk-analysis.md
│
└── examples/
    ├── source-project/
    ├── target-project/
    ├── prompts/
    └── migration-results/
```

---

# 👨‍⚖️ Human-in-the-Loop Principle

```text
AI proposes migration strategies.
Humans validate architecture decisions.
```

AI responsibilities:

- Analyze dependencies
- Generate migration plans
- Suggest replacements
- Assist adaptation
- Identify risks

Human responsibilities:

- Validate architecture boundaries
- Confirm compatibility decisions
- Control migration scope
- Approve final implementation

---

# 📌 Key Principles

## 1. Never migrate blindly

Always verify target capabilities first.

---

## 2. Avoid whole-module migration

Migrate incrementally.

Recommended:

- small features
- isolated workflows
- limited dependency scope

---

## 3. Preserve target architecture

Adapt features to the target system.

Do NOT force source patterns into the target project.

---

## 4. Infrastructure is NOT business logic

Do not directly migrate:

- MQ implementations
- cache frameworks
- ORM frameworks
- auth systems
- thread context systems

These require adaptation.

---

# 📄 License

MIT
