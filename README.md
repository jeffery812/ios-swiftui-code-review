# iOS SwiftUI Code Review Skill

A Codex skill for high-signal iOS code review focused on changed lines only.

## What This Skill Does

- Reviews Swift, SwiftUI, UIKit, and mixed iOS code changes.
- Prioritizes correctness, safety, regressions, architecture, and test coverage.
- Uses a severity model (`P0`-`P3`) and concise actionable findings.
- Applies a bundled Swift style guide as the rule source.

## Included Files

- `SKILL.md`: Main review workflow, scope rules, bias controls, and output format.
- `references/swift-style-guide.md`: Bundled full style guide (source of truth).
- `references/review-checklist.md`: Deduplicated quick review order and project-specific additions.
- `agents/openai.yaml`: UI metadata for skill display and default prompt.

## Review Contract

- Review only touched files/lines.
- Use provided base branch, otherwise default to `master`.
- Avoid speculative or style-only noise unless it impacts readability or correctness.
- End with one recommendation:
  - `approve`
  - `approve with comments`
  - `request changes`

## Example Prompt

Use this skill with a prompt like:

```text
Use $ios-swiftui-code-review to review this PR against master.
Focus on bugs, threading, memory/lifecycle, architectural consistency, and missing tests.
Return Issues & Suggestions, Optional Improvements, and Approval Recommendation.
```

## Publishing to GitHub

1. Ensure this folder is committed:
   - `skills/ios-swiftui-code-review/`
2. Push to your repository.
3. In your repo docs, link to:
   - `skills/ios-swiftui-code-review/SKILL.md`

## Notes

- The style guide is vendored locally at `references/swift-style-guide.md` to avoid external path dependencies.
