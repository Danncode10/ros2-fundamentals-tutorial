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
- Respect student pacing. If the lesson mentions a topic that belongs later in `Lessons/README.md`, gently say that it will be learned later, give only a short beginner-safe summary, and return to the current lesson goal.
- Use the `.claude/agents/student-pacing-teacher.md` agent when the lesson touches advanced or future topics. If subagents are unavailable, manually apply the same pacing rule.
- Never write as if every learner should understand immediately. Use reassuring language such as "You do not need to master this yet" or "This will make more sense after we practice it."
- Use Mermaid Markdown diagrams when they make a concept easier to visualize, especially for ROS 2 node graphs, topic flow, service request/response flow, workspace structure, launch relationships, or lesson sequence. Do not force Mermaid into every lesson.
- Keep Mermaid diagrams simple and compatible with GitHub and VS Code Markdown preview. Prefer `flowchart LR`, `flowchart TD`, or `sequenceDiagram`. Avoid advanced Mermaid features, custom styling, emojis, HTML tags, special symbols, and complicated punctuation in node IDs.
- In Mermaid flowcharts, use plain ASCII node IDs such as `imu_node`, `motor_node`, and `diagnostics_node`. Put readable text in quoted labels, such as `imu_node["IMU node"]`.
- Do not put raw parentheses, slashes, colons, or commas inside unquoted Mermaid labels. If punctuation is needed, quote the full label.
- Always explain the diagram in beginner-friendly prose before or after it. The diagram should support the lesson, not replace the explanation.

## Student Pacing Loop

Before finishing, check whether the generated lesson introduces ideas that are deeper than the matched roadmap section. If it does, run the `.claude/agents/student-pacing-teacher.md` agent. If subagents are unavailable, perform this same review manually:

1. Identify the current matched section.
2. Identify any advanced concept that belongs later in `Lessons/README.md`.
3. Add a respectful student-facing note using this pattern:

```text
That's a good question. We will study that properly in <future lesson or section>, so you do not need to master it yet. For now, the short version is: <one to three beginner-friendly sentences>. In this lesson, focus on <current lesson goal>.
```

4. Keep the explanation short and return to the current lesson steps.

## Mermaid Verification Loop

If the generated lesson includes any `mermaid` fenced code blocks, run the `.claude/agents/mermaid-markdown-verifier.md` agent before finishing. If subagents are unavailable, perform this same review pass manually:

1. Extract every Mermaid block from the Markdown.
2. Check each diagram for GitHub/VS Code-safe syntax:
   - fenced block starts with exactly ```` ```mermaid ```` and ends with ```` ``` ````;
   - graph type is supported, preferably `flowchart LR`, `flowchart TD`, or `sequenceDiagram`;
   - flowchart node IDs are simple ASCII words with letters, numbers, and underscores;
   - labels with spaces or punctuation are wrapped in quotes inside brackets;
   - arrows use common Mermaid forms such as `-->`, `-->|label|`, or `-.->`;
   - no unmatched brackets, quotes, or code fences.
3. Fix any Mermaid issue found and repeat the review once more.
4. If a diagram still seems risky, replace it with a plain Markdown list or table instead of leaving broken Mermaid in the file.

## Completion Response

After creating the file, report:

- the matched README section
- whether a lesson plan was used
- the created file path
- any assumptions made
- whether any future-topic pacing notes were added
- whether Mermaid diagrams were included and verified, or not used
