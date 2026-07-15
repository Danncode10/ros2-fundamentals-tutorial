---
description: Create a 15-item readiness quiz for a ROS 2 lesson.
argument-hint: <Lesson Number>
---

# /make-quiz

Create a short but meaningful quiz for the requested lesson number.

Use this command when the learner wants to check whether the important ideas are understood well enough before moving to the next lesson.

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
Lessons/quizzes/
```

8. Create one Markdown file using this filename format:

```text
<Lesson Number> <Title> Quiz.md
```

Use the lesson number exactly as requested by the user. Use a short, readable title based on the matched lesson, lesson plan, or README section.

## Quiz Purpose

The quiz should check real understanding, not memorization only.

It should help answer:

- Can the learner explain the lesson in beginner language?
- Can the learner recognize the important ROS 2 pieces?
- Can the learner read simple command output or diagrams from the lesson?
- Can the learner avoid the most common wrong mental models?
- Is the learner ready to proceed, or should they review first?

## Required Output File Structure

The generated quiz must use this structure:

````markdown
# <Lesson Number> <Lesson Title> Quiz

## Purpose

This quiz checks whether you understand the most important ideas from <lesson title> before moving on.

## How To Use This Quiz

- Try answering without looking at the lesson first.
- If you miss a question, review that part of the lesson.
- You do not need perfect wording. Focus on the idea.

## Questions

1. **<question>**
2. **<question>**
3. **<question>**
4. **<question>**
5. **<question>**
6. **<question>**
7. **<question>**
8. **<question>**
9. **<question>**
10. **<question>**
11. **<question>**
12. **<question>**
13. **<question>**
14. **<question>**
15. **<question>**

## Answer Key

1. <short beginner-friendly expected answer>
2. <short beginner-friendly expected answer>
3. <short beginner-friendly expected answer>
4. <short beginner-friendly expected answer>
5. <short beginner-friendly expected answer>
6. <short beginner-friendly expected answer>
7. <short beginner-friendly expected answer>
8. <short beginner-friendly expected answer>
9. <short beginner-friendly expected answer>
10. <short beginner-friendly expected answer>
11. <short beginner-friendly expected answer>
12. <short beginner-friendly expected answer>
13. <short beginner-friendly expected answer>
14. <short beginner-friendly expected answer>
15. <short beginner-friendly expected answer>

## Ready To Continue?

- **Ready:** You can answer most questions in your own words and explain the mini-project idea.
- **Review first:** You can recognize words, but cannot explain what they mean or how they connect.
- **Ask for help:** You are stuck on the same concept after reviewing it twice.

## Review Targets

| If you missed... | Review this |
|---|---|
| <question numbers> | <lesson section, concept, command, or diagram> |
````

## Question Requirements

- Create exactly **15 questions**.
- Make every question important for understanding the lesson.
- Prefer short-answer questions over multiple choice.
- Include a few "explain in your own words" questions.
- Include at least one question about a common beginner misunderstanding.
- Include at least one question about a command, output, diagram, or mini-project when the source lesson contains one.
- Include at least one "what is this not?" question when the lesson teaches vocabulary that is easy to misunderstand.
- Do not ask trivia, date questions, or wording-only memorization.
- Do not introduce concepts that are not in the lesson, lesson plan, or roadmap section.
- Keep answers short, respectful, and beginner-friendly.
- If a question touches a future topic, use the student pacing rule from `CLAUDE.md`: mark it as not required for mastery yet and give only a short answer.

## Writing Requirements

- Write like a patient teacher checking understanding before continuing.
- Use simple words.
- Assume the learner is capable but still new.
- Make questions fair: every answer should be discoverable from the lesson, lesson plan, or roadmap section.
- Use bold labels and clean Markdown that previews well in GitHub and VS Code.
- Do not use raw HTML, custom colors, or custom Markdown extensions.
- Keep the quiz focused enough that it can be completed quickly.
- The answer key should teach gently, not scold.
- The readiness section should help the learner decide whether to proceed.

## Completion Response

After creating the file, report:

- the matched README section
- which source material was used
- the created file path
- any assumptions made
