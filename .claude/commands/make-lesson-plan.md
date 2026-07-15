---
description: Create a beginner-friendly ROS 2 lesson plan from Lessons/README.md.
argument-hint: <Lesson Number>
---

# /make-lesson-plan

Create a lesson planning document for the requested lesson number.

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
6. Create the output folder if needed:

```text
Lessons/lesson-plan/
```

7. Create one Markdown file using this filename format:

```text
<Lesson Number> <Title>.md
```

Use the lesson number exactly as requested by the user. Use a short, readable title based on the matched README section. Keep filenames filesystem-friendly.

## Required Output File Structure

The generated lesson plan must include:

````markdown
# <Lesson Number> <Lesson Title>

## Source Section

- Source: `<exact heading from Lessons/README.md>`
- Roadmap summary: <short summary of the matched section>

## Lesson Purpose

Explain why this lesson exists in the course sequence.

## Learning Objectives

- <objective>
- <objective>
- <objective>

## Prerequisite Knowledge

- <what the learner should already know>

## Required Tools

- <tool>
- <tool>

Include a note if the lesson is low-storage friendly. Beginner lessons should avoid heavy tools unless the README section clearly requires otherwise.

## Estimated Time

<estimated beginner-friendly duration>

## Concepts to Teach

- <concept>
- <concept>

## Commands to Demonstrate

```bash
<command>
```

For each command, include a short note explaining what it proves or why it matters.

## Code Artifacts to Create

- `<file or package name>`: <purpose>

## Learner Activities

- <activity>
- <activity>

## Simple Exercise or Mini-Project

Describe one small skill test the learner can complete after the lesson.

Include:

- task
- success criteria
- hint

## Verification Checks

- <ROS 2 CLI command or observable result>
- <expected success sign>

## Beginner Mistakes to Watch For

- <mistake>
- <mistake>

## Troubleshooting Topics

| Symptom | Likely cause | Fix | Verification |
|---|---|---|---|
| <symptom> | <cause> | <fix> | <check> |

## Checkpoint Questions

- <question>
- <question>
- <question>

## Teacher Notes

Guidance for teaching this lesson patiently and clearly.
````

## Writing Requirements

- Write for a beginner.
- Make the lesson plan practical and testable.
- Keep the storage limitation in mind.
- Mention heavier tools only as future work unless the matched section requires them.
- Include a simple exercise or mini-project every time.
- Do not create the full student lesson here. This command creates only the lesson plan.

## Completion Response

After creating the file, report:

- the matched README section
- the created file path
- any assumptions made
