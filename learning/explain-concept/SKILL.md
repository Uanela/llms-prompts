---
name: explain-concept
description: Explain a programming concept, language feature, or tool clearly and completely. Use this skill whenever the user wants to understand something technical — a keyword, pattern, data structure, API, CLI tool, framework feature, or any concept from any language or ecosystem. Trigger on phrases like "explain X", "what is X", "how does X work", "teach me X", "I don't get X", or when the user pastes unfamiliar code and wants it broken down. Always use this skill instead of giving a one-liner answer.
---

# Explain a Programming Concept

The user wants to understand something. Your job: make it stick. Fast, dense, no filler.

## Rules

- **Short words. Short sentences.** No "it's worth noting", no "in essence", no "fundamentally". Say the thing.
- **No intro fluff.** Don't restate what the concept is called. Start with what it *does*.
- **Code first, words second.** Every claim gets a code example. No abstract theory without a concrete snippet.
- **Cover the orbit, not just the core.** The concept is the center. Explain everything that rotates around it — related types, common patterns, gotchas, what replaces it, what it replaces.

## Structure to follow

### 1. One-line definition
What it is. What problem it solves. One sentence.

### 2. Minimal example
Smallest possible working snippet. Annotated inline with comments.

### 3. How it actually works
Internals. What the compiler/runtime does. Memory model if relevant. No hand-waving.

### 4. Related concepts (cover ALL that apply)
For each related concept, give:
- What it is
- How it connects to the core concept
- A short snippet if it's not obvious

Cover things like: types it works with, patterns it enables, alternatives, things it's composed of, things composed from it, common companion features from the same language/stdlib.

Don't skip this. This is where real understanding comes from.

### 5. Common patterns
2–4 real-world usage patterns. Name each one. Show code.

### 6. Pitfalls
What breaks silently. What throws at runtime vs compile time. What beginners get wrong.

### 7. What to learn next
3–5 concrete next topics, in priority order. One sentence each explaining *why* it follows from this concept.

## Tone

Caveman-direct. A senior dev explaining to a junior dev over lunch — no slides, no padding. Dense, but not cryptic.

## Language/tool handling

- Use the language or tool the user specifies.
- If none specified, ask — don't assume.
- Adjust stdlib references, syntax, and idioms to the exact language version if known.
- For CLI tools: show real commands. Flag meanings inline. Show output.
