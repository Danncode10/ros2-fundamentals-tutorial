---
description: Create a complete beginner-facing ROS 2 lesson from the roadmap and optional lesson plan.
argument-hint: <Lesson Number>
---

# /make-lesson

Create the actual student-facing lesson for the requested lesson number.

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
   - Accept formats such as `1`, `1.1`, `Module 1`, `Phase 1`, or `Section 1.1`.
   - If the match is ambiguous, list the possible matches and ask the user to choose.
   - If there is no match, explain what lesson numbers are available from the README.
6. Check `Lessons/lesson-plan/` for a matching lesson plan.
   - If one exists, read it and use it as guidance.
   - If one does not exist, generate the lesson directly from `Lessons/README.md` and mention that no lesson plan file was found.
7. Create the output folder if needed:

```text
Lessons/lessons/
```

8. Create one Markdown file using this filename format:

```text
<Lesson Number> <Title>.md
```

Use the lesson number exactly as requested by the user. Use a short, readable title based on the matched README section or lesson plan. Keep filenames filesystem-friendly.

## Required Output File Structure

The generated actual lesson must include:

````markdown
# <Lesson Number> <Lesson Title>

## Lesson Goal

By the end of this lesson, you will be able to <clear beginner outcome>.

## Why This Matters

Explain why this concept matters in ROS 2 and, when useful, robotics.

## Before You Start

List prerequisites, required tools, and storage notes.

## New Words

Explain beginner vocabulary before using it heavily.

## Big Idea

Give a plain-language explanation of the core concept.

## Step 1: <Action>

Explain the action.

```bash
<exact command>
```

Explain what the command does and what success looks like.

## Step 2: <Action>

Continue with small steps.

## Minimal Code

When code is required, provide the smallest useful code example.

```python
<code>
```

Explain the important lines.

## Run It

```bash
<command>
```

## Verify It

Use ROS 2 CLI commands when relevant.

```bash
<command>
```

Expected success signs:

- <sign>
- <sign>

## Common Mistakes

- <mistake and explanation>
- <mistake and explanation>

## Troubleshooting

| Symptom | Likely cause | Fix | How to verify |
|---|---|---|---|
| <symptom> | <cause> | <fix> | <check> |

## Simple Exercise or Mini-Project

Give the learner one small task to test their skill.

Include:

- task
- requirements
- success criteria
- optional hint

## Recap

- <key idea>
- <key idea>
- <key idea>

## Checkpoint Questions

- <question>
- <question>
- <question>
````

## Writing Requirements

- Write as a complete beginner tutorial.
- Be patient, concrete, and practical.
- Explain jargon the first time it appears.
- Include exact commands and expected success signs.
- Include a simple exercise or mini-project every time.
- Keep early lessons low-storage friendly.
- Do not require Gazebo, Navigation2, MoveIt, Docker, YOLO, AI packages, large simulation worlds, or full desktop stacks in beginner lessons.
- Mention heavy tools only as future work unless the roadmap clearly says otherwise.
- Prefer tiny working examples before larger abstractions.
- Make it possible for the learner to test whether they succeeded.

## Completion Response

After creating the file, report:

- the matched README section
- whether a lesson plan was used
- the created file path
- any assumptions made
