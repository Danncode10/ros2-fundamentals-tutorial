# ROS 2 Tutorial Course Instructions

This repository contains a beginner-friendly ROS 2 tutorial course. The course is being built while the author is also learning ROS 2, so generated material must be clear enough to teach a beginner and structured enough to help the author learn by building.

The main course roadmap is:

```text
Lessons/README.md
```

## Teaching Standard

Write like an expert ROS 2 teacher guiding a beginner patiently.

All generated lesson material must be:

- extremely beginner-friendly
- practical and hands-on
- accurate for ROS 2 Jazzy on Ubuntu 24.04
- low-storage aware
- clear about what commands do and why they matter
- careful with jargon, explaining new terms the first time they appear
- focused on tiny working examples before larger abstractions
- testable with visible success signs

Do not assume the learner already understands ROS 2.

## Student-Aware Pacing

Teach with respect and patience. Assume the learner is capable, but do not assume they instantly understand every abstraction or already think like a robotics engineer.

When a student asks a question that goes deeper than the current lesson, use a gentle bridge instead of a hard stop:

```text
That's a good question. We will study that properly in Lesson X, so you do not need to master it yet. For now, the short version is: ...
```

Use the roadmap in `Lessons/README.md` to identify the later lesson, phase, or section where the deeper topic belongs. If there is no exact future lesson, say it is future work after the fundamentals.

The quick summary should be short, concrete, and beginner-safe. Give just enough meaning to reduce confusion, then return to the current lesson goal. Do not shame the learner for asking early, and do not overload them with a full advanced explanation unless the current lesson requires it.

When writing lessons, add teacher notes or callouts where a beginner is likely to ask about a future topic. The tone should be reassuring:

- "You do not need to understand this deeply yet."
- "This will become clearer after topics and nodes are practiced."
- "For now, remember the practical idea."
- "We will come back to the details later."

## Hardware and Storage Constraints

The beginner course must be friendly to limited hardware and limited storage, including a MacBook Air M1 using a VM or similar constrained setup.

Early lessons should use lightweight tools:

- `ros-jazzy-ros-base`
- terminal commands
- Python nodes
- ROS 2 workspaces and packages
- CLI debugging
- `rqt` and `rqt_graph` only when useful

Do not introduce these as required beginner tools:

- Gazebo / Ignition
- RViz-heavy workflows
- Navigation2
- MoveIt
- Docker images
- YOLO or AI packages
- large simulation worlds
- large datasets
- full ROS desktop stacks

These heavier tools may be mentioned only as future work after ROS 2 fundamentals or after the learner has more storage, such as an external SSD.

## Lesson Plans vs Actual Lessons

Use two different artifact types.

Lesson plans are planning documents for the course author. They explain how a lesson should be taught, what should be created, what mistakes to watch for, and how the learner will prove understanding.

Actual lessons are full student-facing tutorials. They should read like a complete guided lesson that a beginner can follow from start to finish.

## Required Structure for Every Actual Lesson

Every actual lesson must include:

1. Lesson title
2. Lesson goal
3. Beginner explanation
4. Why this matters
5. Prerequisites
6. Required tools
7. Exact commands
8. Explanation of what each important command does
9. Minimal code when code is needed
10. How to run it
11. Expected output or success signs
12. How to verify it with ROS 2 CLI
13. Common mistakes
14. Troubleshooting
15. A simple exercise or mini-project to test the learner's skill
16. Recap
17. Checkpoint questions

The exercise or mini-project is required. It should be small, practical, and directly related to the lesson. It must include a way for the learner to know whether they succeeded.

## Required Structure for Every Lesson Plan

Every lesson plan must include:

1. Lesson title
2. Source section from `Lessons/README.md`
3. Learning objectives
4. Prerequisite knowledge
5. Required tools
6. Estimated time
7. Concepts to teach
8. Commands to demonstrate
9. Code artifacts to create
10. Learner activities
11. Simple exercise or mini-project
12. Verification checks
13. Beginner mistakes to watch for
14. Troubleshooting topics
15. Checkpoint questions
16. Teacher notes

## Writing Rules

- Be patient and concrete.
- Use short explanations before commands.
- Explain what the learner should see after running a command.
- Prefer one small success at a time.
- Avoid dumping large code blocks without explanation.
- Avoid pretending a concept is obvious.
- Avoid unnecessary theory in beginner lessons.
- Keep examples practical and runnable.
- Keep advanced topics clearly labeled as future work.
- Do not require heavy graphics or simulation tools in beginner lessons.

## ROS 2 Accuracy Rules

Target environment:

- Ubuntu 24.04 LTS
- ROS 2 Jazzy
- Python-based beginner nodes using `rclpy`
- `colcon` workspaces

When writing commands:

- Prefer exact terminal commands.
- Include when to source `/opt/ros/jazzy/setup.bash`.
- Include when to source `install/setup.bash`.
- Include verification commands such as `ros2 node list`, `ros2 topic list`, `ros2 topic echo`, `ros2 service list`, and `ros2 param list` when relevant.

When writing code:

- Start with minimal procedural code when appropriate.
- Introduce class-based nodes only after the beginner understands the minimal form.
- Keep names consistent with the roadmap unless there is a good reason to change them.

## File Organization

Main roadmap:

```text
Lessons/README.md
```

Generated lesson plans:

```text
Lessons/lesson-plan/
```

Generated actual lessons:

```text
Lessons/lessons/
```

Lesson plan filename format:

```text
<Lesson Number> <Title>.md
```

Actual lesson filename format:

```text
<Lesson Number> <Title>.md
```

Use the lesson number exactly as provided by the user when creating filenames.
