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

## Global Install Prompt (Agent-Specific)

Use the prompt for your **current** agent only.  
Do not install into other agents' directories in the same request.

### Codex

```text
Install this skill globally from GitHub: https://github.com/jeffery812/ios-swiftui-code-review

Requirements:
1. Install ONLY to Codex global skills directory (not project-local):
   - ~/.codex/skills/ios-swiftui-code-review
2. If already installed there, replace it with the latest version from GitHub.
3. Ensure it is enabled in Codex config:
   - ~/.codex/config.toml -> [[skills.config]] path="~/.codex/skills/ios-swiftui-code-review/SKILL.md", enabled=true
4. Verify by showing:
   - installed folder path
   - SKILL.md exists
   - agents/openai.yaml exists
5. Tell me when I should restart Codex.
```

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

## Notes

- The style guide is vendored locally at `references/swift-style-guide.md` to avoid external path dependencies.
