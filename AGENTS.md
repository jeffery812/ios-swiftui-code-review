# AGENTS.md

## Purpose

This repository defines an iOS SwiftUI code-review skill.  
Use this guide when an agent is asked to review Swift/SwiftUI/UIKit changes.

## Scope

- Review only touched files and changed lines.
- Prioritize correctness, regression risk, crash risk, threading, lifecycle, and test gaps.
- Avoid speculative, style-only, or large-refactor commentary unless there is clear risk.

## Repository Map

- `SKILL.md`: Primary review contract and reporting format.
- `references/swift-style-guide.md`: Source of truth for Swift style rules.
- `references/review-checklist.md`: Fast review order and project-specific additions.
- `agents/openai.yaml`: UI metadata and default prompt.

## Required Review Workflow

1. Determine base branch.
2. If not specified, default to `master`.
3. Read only diff/touched files.
4. Load `references/swift-style-guide.md`.
5. Use this review order:
   1. Behavior correctness and safety.
   2. Crash risk, memory ownership, lifecycle, concurrency/threading.
   3. SwiftUI state ownership and side effects.
   4. Architectural consistency with existing patterns.
   5. Style-guide compliance (only meaningful, non-noisy issues).
   6. Missing or weak tests for user-critical paths and bug fixes.

## SwiftUI-Specific Checks

- State ownership is explicit and correct (`@State`, `@Binding`, `@StateObject`, `@ObservedObject`, `@Environment`).
- No side effects inside `body`.
- Stable identity usage in lists/collections.
- Main-thread UI updates.
- No obvious recomposition/performance pitfalls in changed code.

## Style Rule Application

- Cite section titles from `references/swift-style-guide.md` when flagging style issues.
- Respect project-specific additions from `references/review-checklist.md`:
  - Doc comments should use `///`.
  - Implicit returns only for single-expression bodies.

## Severity Model

- `P0`: Crash, data loss, privacy/security issue, production blocker.
- `P1`: High-confidence functional bug or major regression risk.
- `P2`: Maintainability/performance issue likely to cause defects.
- `P3`: Minor readability/consistency issue.

## Required Output Format

Use this exact section order:

1. `Issues & Suggestions` (findings first, sorted by `P0` -> `P3`, include file + line).
2. `Optional Improvements` (non-blocking polish only).
3. `Approval Recommendation` with one of:
   - `approve`
   - `approve with comments`
   - `request changes`

If no findings exist, state that explicitly and mention residual risks or test gaps.

## Agent Behavior Rules

- Be concise and actionable.
- Do not invent missing context; note uncertainty briefly.
- Do not rewrite unchanged architecture unless current changes introduce concrete risk.
- Focus on changed code impact, not generic best-practice advice.
