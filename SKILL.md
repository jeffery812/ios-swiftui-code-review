---
name: ios-swiftui-code-review
description: Review iOS SwiftUI, UIKit, and mixed Swift code for correctness, regression risk, architecture, and style-guide compliance. Use when asked to review PRs, diffs, or files in Apple-platform projects, especially when enforcing the bundled Swift style guide in references/swift-style-guide.md.
---

# iOS SwiftUI Code Review

## Role

Act as an expert iOS engineer across Swift, SwiftUI/UIKit, architecture, concurrency, memory, and testing.

## Load Review Context

1. Use the provided base branch; if none is provided, use `master`.
2. Read only the touched files and changed lines.
3. Read `references/swift-style-guide.md`.
4. If the guide file is unavailable, report it and continue with Swift/SwiftUI best practices.
5. If tests or other context are missing, note that briefly instead of guessing.

## Review Workflow

1. Check behavior and correctness first.
2. Check crash risk, threading, state management, memory ownership, and lifecycle issues.
3. Check architectural consistency with existing patterns and flag meaningful deviations.
4. Check SwiftUI architecture:
   - Prefer clear state ownership (`@State`, `@Binding`, `@StateObject`, `@ObservedObject`, `@Environment`).
   - Flag side effects in `body` and unstable identity usage.
   - Flag view recomposition and performance pitfalls.
5. Check Swift and iOS best practices:
   - Ensure UI updates happen on the main thread.
   - Prefer async/await and sensible immutability.
   - Flag meaningful unnecessary complexity.
6. Check style-guide compliance using `references/review-checklist.md`.
7. Check tests:
   - Flag missing tests for bug fixes, reducers/view models, and user-critical flows.
   - Flag flaky or non-deterministic test patterns.

## Bias Controls

- Avoid style-only nitpicks and generic best-practice advice unless clearly applicable.
- Avoid large rewrite or tech-debt commentary unless the current change introduces concrete risk.
- Raise security issues only when concrete.
- Prefer concise, actionable notes and avoid speculative remarks.

## Reporting Format

1. Report findings first, sorted by severity (`P0` to `P3`), and focus only on changed code.
2. For each issue, include:
   - File name/path.
   - Exact line number (or the smallest precise line range when needed).
   - Specific code context (symbol/function/view name).
3. For each issue, explain concrete impact and specific fix direction with as much useful detail as possible.
4. Group concise actionable bullets under `Issues & Suggestions`.
5. Put non-blocking polish under `Optional Improvements`.
6. End with `Approval Recommendation`: `approve`, `approve with comments`, or `request changes`.
7. If no findings exist, state that explicitly and list residual risks or test gaps.

## Severity Guide

- `P0`: Crash, data loss, security/privacy issue, or production blocker.
- `P1`: High-confidence functional bug or major regression risk.
- `P2`: Maintainability/performance issues likely to cause defects.
- `P3`: Minor style, readability, or consistency issue.
