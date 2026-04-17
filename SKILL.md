---
name: execution-prompt-refiner
description: Refine rough user requests into precise, execution-ready prompts while preserving the original goal, constraints, tone, and important domain terms. Use when Codex needs to transform ambiguous instructions, mixed Chinese and English shorthand, or high-level requests into an actionable brief with scope, constraints, inputs, and expected output.
---

# Execution Prompt Refiner

Refine the user's rough request into a prompt another execution agent can act on immediately. Preserve intent, non-negotiable constraints, important domain vocabulary, and rollout-sensitive details.

## Workflow

1. Extract the core task, desired outcome, and explicit constraints.
2. Identify only the missing context that materially affects correct execution.
3. Replace vague wording with operational language.
4. Organize the rewritten prompt into a clean brief with:
   - task or objective
   - scope
   - constraints
   - inputs or context
   - expected output
5. Return the rewritten prompt, adding `Assumptions` or `Missing Context` only when they are necessary.

## Guardrails

- Do not change the user's goal.
- Do not invent requirements unless needed for safe execution.
- Keep assumptions minimal and state them clearly.
- Preserve framework names, file paths, versions, APIs, rollout risks, and other domain-specific terms.
- Normalize mixed Chinese and English shorthand into clearer language without stripping important terminology.
- Prefer concise, execution-oriented wording over explanation.

## Output Shape

Use a clean execution brief that another agent can follow directly.

```text
[Execution-ready prompt]

Assumptions
- ...

Missing Context
- ...
```

Omit `Assumptions` if none were needed. Omit `Missing Context` if the request is executable as written.

## Typical Transformations

- Turn "optimize this page" into explicit UI, performance, and scope goals.
- Turn "fix the payment flow" into concrete entry points, expected behavior, and validation needs.
- Turn mixed shorthand into a coherent brief while retaining important product and technical terms.
