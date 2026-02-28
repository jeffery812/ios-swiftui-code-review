# Swift Style Review Checklist (Deduplicated)

Source of truth:
- `references/swift-style-guide.md`

Use this file as a review flow and section index. Do not restate rules already defined in the style guide.

## Fast Review Order

1. Correctness and safety (`Correctness`, `Memory Management`, `Golden Path`).
2. Naming and API clarity (`Naming`, `Functions vs Methods`).
3. Code organization (`Code Organization`, `Access Control`).
4. Formatting and readability (`Spacing`, `Comments`, `Function Declarations`, `Function Calls`, `Closure Expressions`).
5. Swift language usage (`Types`, `Optionals`, `Type Inference`, `Syntactic Sugar`, `Control Flow`, `Semicolons`, `Parentheses`).

## Reviewer Output Rule

- When raising a style issue, cite the matching section title from `references/swift-style-guide.md`.
- Avoid style-only comments unless they improve readability or prevent defects.

## Project-Specific Additions

- Documentation comments: use `///`; keep each doc-comment line single-line, and use multiple `///` lines for multi-line docs.
- Implicit returns: allow only for single-expression bodies; require explicit `return` for multi-statement bodies.
