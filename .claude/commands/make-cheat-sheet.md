---
description: Create a short ROS 2 command cheat sheet with clear command definitions.
argument-hint: <Lesson Number>
---

# /make-cheat-sheet

Create a short cheat sheet for the requested lesson number. The cheat sheet must focus on commands, but every command must have a clear beginner definition.

User argument:

```text
$ARGUMENTS
```

## Procedure

1. Read `AGENTS.md`.
2. Read `CLAUDE.md`.
3. Read `Lessons/README.md`.
4. Treat `$ARGUMENTS` as the requested lesson number, module number, phase number, or section number.
5. Find the best matching lesson or section in `Lessons/README.md`.
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

The generated cheat sheet must be short, practical, and command-focused. It must not become a full lesson, but it also must not list commands without explaining them.

````markdown
# <Lesson Number> <Lesson Title> Cheat Sheet

## Main Idea

<one short sentence about what the lesson teaches>

## Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `<command>` | <plain-English definition> | <when to type it> | <what success looks like> |

## Tiny Terms

| Term | Meaning |
|---|---|
| <term> | <short beginner meaning> |

## Remember

- <one key warning or habit>
- <one key warning or habit>
````

## Writing Requirements

- Keep the cheat sheet short enough to review while the terminal is open.
- Do not create a full lesson, recap, or troubleshooting guide.
- Every command must have a definition: what the command means, not only what it checks.
- Prefer tables for command definitions.
- Include only commands that appear in the source lesson or are directly required by it.
- Include only the most important vocabulary, usually 3 to 8 terms.
- Keep command definitions short, concrete, and beginner-friendly.
- Avoid diagrams unless the lesson has no real commands, such as Lesson 0.
- Avoid self-check questions unless the user explicitly asks for study questions.
- Avoid long code blocks. Use file names and console script lines only when the lesson depends on remembering them.
- Keep the whole cheat sheet roughly 30 to 90 lines. If a command table gets too wide, split it into two smaller tables.
- Keep storage and beginner constraints in mind.
- Mention heavy tools only if the lesson itself mentions them as future work.
- Avoid adding new concepts that are not in the lesson, lesson plan, or roadmap section.

## Completion Response

After creating the file, report:

- the matched README section
- which source material was used
- the created file path
- any assumptions made
