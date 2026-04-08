I need you to generate git add and git commit commands from a unified diff. The diff shows changes across multiple files. Generate one `git add` and `git commit` command per logical change group, not one per file.

**Rules:**
- Group related changes together (same feature, same module, same purpose)
- **DO NOT be over-granular** — err on the side of fewer, larger commits rather than many tiny ones. If changes are part of the same feature or logical unit (even across different file types), group them together
- Use present tense, imperative style for commit messages (e.g., "fix:", "feat:", "refactor:", "test:", "chore:", "docs:")
- Keep messages under 72 characters for the subject line
- **Path handling:** Any path containing parentheses `(` or `)` MUST be wrapped in double quotes (e.g., `"apps/frontend/app/admin/(main)/file.ts"`)
- Order commits by dependency — if file A changes depend on file B changes, commit file B first
- Skip whitespace-only changes when grouping
- Do not include binary files unless explicitly changed
- **Output format:** Generate ONLY the git commands. Do not add commentary, explanations, or markdown formatting around the commands. Just output the raw bash commands, each on a new line.

**Examples of GOOD grouping (not over-granular):**
- All changes to a new feature (controller + service + routes + tests) → ONE commit
- All dependency updates across multiple package files → ONE commit
- Error handling system (base classes + middleware + helpers) → ONE commit

**Examples of BAD grouping (over-granular):**
- Splitting a new feature into separate commits for controller, service, and routes
- Creating separate commits for each utility function in a module
- Committing each file individually when they serve the same purpose

**Example output format:**
```bash
git add "path/to/file1.ts" "path/to/file2.ts"
git commit -m "feat(module): add feature description"

git add path/to/file3.ts
git commit -m "fix(module): correct something"
```
