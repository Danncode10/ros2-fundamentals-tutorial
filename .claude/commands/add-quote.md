---
description: Add a student understanding note under a matching line in a lesson.
argument-hint: <lesson> | <anchor text> | <student note>
---

# /add-quote

Add the user's understanding, quote, or reminder directly below a matching part of a student-facing lesson.

Use this when the user wants to preserve something they said during chat inside the lesson, like a personal understanding note, without repeating the full editing prompt every time.

User argument:

```text
$ARGUMENTS
```

## Procedure

1. Read `AGENTS.md`.
2. Read `CLAUDE.md`.
3. Parse `$ARGUMENTS` as:

```text
<lesson> | <anchor text> | <student note>
```

Examples:

```text
Lesson 0 | Topic: A named communication channel | A topic is basically where messages are sent.
```

```text
0 | Publisher: | Publishing means the node is speaking on the topic.
```

4. Find the best matching lesson file in `Lessons/lessons/`.
   - Accept lesson references such as `Lesson 0`, `0`, `0 Orientation`, or an exact filename.
   - If one clear match exists, use it.
   - If multiple lessons match, list the candidates and ask the user to choose.
   - If no lesson matches, explain which lesson files are available.
5. Find the best matching anchor text inside the lesson.
   - Prefer an exact text match.
   - If there is no exact match, search for a close matching heading, vocabulary term, sentence, or paragraph.
   - If the anchor is ambiguous, list the possible matches and ask the user to choose.
6. Add the student note directly below the matched anchor paragraph.
7. Format the inserted note as a Markdown blockquote callout so it is easy to see in GitHub and VS Code preview:

```markdown
> **Student note**
>
> <student note>
```

8. If the note is the user's rough wording, lightly clean grammar only when it improves clarity. Preserve the user's meaning and beginner voice.
9. Do not rewrite the whole lesson unless needed for the inserted note to make sense.
10. Keep the note respectful and beginner-friendly.

## If The User Does Not Provide All Three Parts

If the user says something like:

```text
add this under Topic: <student note>
```

Infer the current or most recently discussed lesson when it is obvious from context. If the lesson is not obvious, ask which lesson file to edit.

If the anchor is obvious but the note is not, ask for the exact note to add.

## Writing Rules

- Use this command for student-facing lessons in `Lessons/lessons/`, not lesson plans, unless the user explicitly asks for a lesson plan.
- Insert the note below the relevant paragraph, not at the bottom of the file.
- Keep the note short, usually one to three sentences.
- Use bold labels and blockquote callouts instead of colored text, because color is not reliable in plain GitHub Markdown or VS Code Markdown preview.
- Prefer plain beginner language over expert wording.
- Do not add advanced ROS 2 explanations unless the current lesson already teaches that topic.
- If the note asks about a future topic, use the student pacing rule from `CLAUDE.md`.
- Do not add Mermaid diagrams for this command unless the user explicitly asks.

## Completion Response

After editing the file, report:

- the lesson file edited
- the anchor text used
- the student note added
- any assumptions made
