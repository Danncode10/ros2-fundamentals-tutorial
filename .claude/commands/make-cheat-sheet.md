---
description: Create a one-glance ROS 2 cheat sheet for a lesson.
argument-hint: <Lesson Number>
---

# /make-cheat-sheet

Create a short review cheat sheet for the requested lesson number.

User argument:

```text
$ARGUMENTS
```

## Procedure

1. Read `AGENTS.md`.
2. Read `CLAUDE.md`.
3. Read `Lessons/README.md`.
4. Treat `$ARGUMENTS` as the requested lesson number, module number, phase number, or section number.
5. Find the best matching section in `Lessons/README.md`.
   - Accept formats such as `0`, `Lesson 0`, `1.1`, `Module 1`, `Phase 1`, or `Section 1.1`.
   - If the match is ambiguous, list the possible matches and ask the user to choose.
   - If there is no match, explain what lesson numbers are available from the README.
6. Look for matching source material in this order:
   - `Lessons/lessons/`
   - `Lessons/lesson-plan/`
   - `Lessons/README.md`
7. Create the output folder if needed:

```text
Lessons/cheat-sheet/
```

8. Create one Markdown file using this filename format:

```text
<Lesson Number> <Title> Cheat Sheet.md
```

Use the lesson number exactly as requested by the user. Use a short, readable title based on the matched lesson, lesson plan, or README section.

## Required Output File Structure

The generated cheat sheet must be short and easy to scan:

````markdown
# <Lesson Number> <Lesson Title> Cheat Sheet

## Big Picture

- <one to three bullets only>

## Must Remember

- <key idea>
- <key idea>
- <key idea>

## Key Words

| Word | Quick meaning |
|---|---|
| <term> | <short meaning> |

## Tiny Diagram Or Mental Model

<small ASCII list, small Mermaid diagram, or short analogy only if useful>

## Commands To Recognize

```bash
<command>
```

- <what it checks in one short phrase>

## Quick Self-Check

- <question>
- <question>
- <question>
````

## Writing Requirements

- Keep the cheat sheet short enough to review in one glance.
- Do not create a full lesson or detailed explanation.
- Prefer bullets, short tables, and bold labels.
- Include only the highest-value commands.
- Include only the most important vocabulary.
- Use beginner-friendly language.
- Keep storage and beginner constraints in mind.
- Mention heavy tools only if the lesson itself mentions them as future work.
- If a diagram is useful, keep it tiny. For ROS 2 architecture diagrams, read and follow `Lessons/Dann ROS 2 Graph.md`; otherwise use the simplest visual format.
- Do not include long code blocks unless the lesson absolutely depends on a tiny snippet.
- Avoid adding new concepts that are not in the lesson, lesson plan, or roadmap section.

## Completion Response

After creating the file, report:

- the matched README section
- which source material was used
- the created file path
- any assumptions made
