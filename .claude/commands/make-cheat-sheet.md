---
description: Create a command-first ROS 2 cheat sheet for a lesson.
argument-hint: <Lesson Number>
---

# /make-cheat-sheet

Create a short command cheat sheet for the requested lesson number.

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

The generated cheat sheet must be very short and command-first. It is **not** a mini-lesson. It should help the learner remember what to type and what each command proves.

````markdown
# <Lesson Number> <Lesson Title> Cheat Sheet

## Lesson Reminder

- <one sentence only>

## Commands

```bash
<command>
```

- <what this command does or proves in one short phrase>

## Tiny Terms

| Word | Quick meaning |
|---|---|
| <term> | <short meaning> |

## Remember

- <one key warning or success sign>
- <one key warning or success sign>
````

## Writing Requirements

- Keep the cheat sheet short enough to review quickly while the terminal is open.
- Do not create a full lesson or detailed explanation.
- Prefer commands over explanations.
- Include only commands that appear in the source lesson or are directly required by it.
- Include only the most important vocabulary, usually 3 to 8 terms.
- Avoid diagrams unless the lesson has no real commands, such as Lesson 0.
- Avoid self-check questions unless the user explicitly asks for study questions.
- Avoid long code blocks. Use file names and console script lines only when the lesson depends on remembering them.
- Keep most command explanations to one line.
- Keep the whole cheat sheet roughly 30 to 80 lines. If a lesson has many commands, group related commands in one code block.
- Use beginner-friendly language.
- Keep storage and beginner constraints in mind.
- Mention heavy tools only if the lesson itself mentions them as future work.
- Avoid adding new concepts that are not in the lesson, lesson plan, or roadmap section.

## Completion Response

After creating the file, report:

- the matched README section
- which source material was used
- the created file path
- any assumptions made
