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
- Improve Markdown readability for GitHub and VS Code preview. Use bold labels for key planning labels, teacher notes, and important reminders, such as `**Teacher note:**`, `**Future topic:**`, or `**Success sign:**`.
- Use Markdown blockquote callouts for important teacher reminders or student-facing notes that should stand apart:

```markdown
> **Teacher note**
>
> <short planning reminder>
```

- Do not rely on colored text, raw HTML styling, or custom Markdown extensions because they may not render consistently in GitHub or VS Code.
- Use indentation, short paragraphs, bullets, and tables to make plans easier to scan.
- Respect student pacing. If the lesson plan mentions a topic that belongs later in `Lessons/README.md`, add a teacher note that gently defers the full explanation to that future lesson or section.
- Use the `.claude/agents/student-pacing-teacher.md` agent when the plan touches advanced or future topics. If subagents are unavailable, manually apply the same pacing rule: briefly summarize the future topic, name where it will be learned later when possible, and return focus to the current lesson.
- Use Mermaid Markdown diagrams when they make a concept easier to visualize, especially for ROS 2 node graphs, topic flow, service request/response flow, workspace structure, or lesson sequence. Do not force Mermaid into every lesson plan.
- Keep Mermaid diagrams simple and compatible with GitHub and VS Code Markdown preview. Prefer `flowchart LR`, `flowchart TD`, or `sequenceDiagram`. Avoid advanced Mermaid features, custom styling, emojis, HTML tags, special symbols, and complicated punctuation in node IDs.
- In Mermaid flowcharts, use plain ASCII node IDs such as `imu_node`, `motor_node`, and `diagnostics_node`. Put readable text in quoted labels, such as `imu_node["IMU node"]`.
- Do not put raw parentheses, slashes, colons, or commas inside unquoted Mermaid labels. If punctuation is needed, quote the full label.
- For ROS 2 system architecture diagrams, prefer a consistent visual convention:
  - read and follow `Lessons/Dann ROS 2 Graph.md`;
  - call the course convention a **Dann ROS 2 Graph** when teaching beginner ROS 2 architecture diagrams;
  - explain that it is a course drawing convention, not an official ROS 2 standard name;
  - include a short legend explaining the shapes and arrow styles.
- For advanced ROS 2 lesson plans, use optional Dann ROS 2 Graph symbols from `Lessons/Dann ROS 2 Graph.md` only when the lesson actually needs them.
- Do not force the ROS 2 node/topic/service convention onto non-ROS diagrams. For non-ROS visuals, choose the simplest Mermaid diagram type that explains the idea clearly.

## Student Pacing Loop

Before finishing, check whether the generated lesson plan introduces ideas that are deeper than the matched roadmap section. If it does, run the `.claude/agents/student-pacing-teacher.md` agent. If subagents are unavailable, perform this same review manually:

1. Identify the current matched section.
2. Identify any advanced concept that belongs later in `Lessons/README.md`.
3. Add a respectful teacher note using this pattern:

```text
This is a good question, but students do not need to master it yet. It will be taught in <future lesson or section>. For now, the short version is: <brief beginner-safe summary>.
```

4. Keep the main plan focused on the current lesson objective.

## Mermaid Verification Loop

If the generated lesson plan includes any `mermaid` fenced code blocks, run the `.claude/agents/mermaid-markdown-verifier.md` agent before finishing. If subagents are unavailable, perform this same review pass manually:

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
- the created file path
- any assumptions made
- whether any future-topic pacing notes were added
- whether Mermaid diagrams were included and verified, or not used
