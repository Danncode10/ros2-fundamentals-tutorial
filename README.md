# ROS 2 Fundamentals Tutorial

A beginner-friendly ROS 2 course for learning the core ideas behind modern robot software.

This repository is designed for learners who are new to ROS 2 and want a practical, low-storage path into robotics programming. The course starts with the essentials: terminals, workspaces, packages, Python nodes, topics, services, custom interfaces, parameters, launch files, and command-line debugging.

The goal is not to install every robotics tool on day one. The goal is to understand how ROS 2 systems are built, tested, and debugged from the ground up.

---

## What You Will Learn

By the end of the beginner course, you should be able to:

- set up a lightweight ROS 2 Jazzy environment
- create and build ROS 2 workspaces
- create Python ROS 2 packages
- write simple ROS 2 nodes
- publish and subscribe to topics
- create and call services
- define custom messages and services
- use parameters for runtime configuration
- write launch files to start multiple nodes
- inspect and debug a ROS 2 graph from the terminal
- complete a small integrated ROS 2 project

---

## Why This Course Exists

ROS 2 can feel overwhelming at the beginning because many tutorials quickly jump into simulation, visualization, navigation, robot models, and large toolchains.

This course takes a smaller and clearer route:

1. Learn the communication model first.
2. Build tiny working examples.
3. Verify everything with ROS 2 CLI tools.
4. Add visual debugging only when it helps.
5. Save heavy robotics tools for later.

This makes the course friendlier for beginners and for laptops or virtual machines with limited storage.

---

## Low-Storage First

The beginner path starts with:

```text
ros-jazzy-ros-base
```

and later adds only small visualization tools when needed:

```text
ros-jazzy-rqt
ros-jazzy-rqt-graph
```

The early course does not require:

- Gazebo / Ignition
- Navigation2
- MoveIt
- Docker images
- YOLO or AI packages
- large simulation worlds
- full ROS desktop stacks

Those tools are important, but they belong after the fundamentals are comfortable or when more storage is available.

---

## Recommended Environment

The course targets:

| Tool | Version |
|---|---|
| Ubuntu | 24.04 LTS |
| ROS 2 | Jazzy |
| Language | Python |
| Build tool | colcon |
| Beginner install | ros-jazzy-ros-base |

If you are on a small-storage machine, start with the base install and avoid full desktop robotics stacks at first.

---

## Start Here

1. Install and verify the lightweight ROS 2 setup:

   [Installation-Guides/01 ROS 2 Jazzy Base Install and Verification.md](Installation-Guides/01%20ROS%202%20Jazzy%20Base%20Install%20and%20Verification.md)

2. Read the course roadmap:

   [Lessons/README.md](Lessons/README.md)

3. Begin with Module 1:

   ROS 2 Environment and Workspace

---

## Course Structure

```text
.
├── Installation-Guides/
│   └── 01 ROS 2 Jazzy Base Install and Verification.md
├── Lessons/
│   ├── README.md
│   ├── lesson-plan/
│   └── lessons/
├── AGENTS.md
├── CLAUDE.md
└── README.md
```

### Important Folders

| Path | Purpose |
|---|---|
| `Installation-Guides/` | Setup and verification guides |
| `Lessons/README.md` | Main course roadmap and lesson plan |
| `Lessons/lesson-plan/` | Planning documents for future lessons |
| `Lessons/lessons/` | Student-facing lessons |
| `AGENTS.md` | Instructions for coding agents |
| `CLAUDE.md` | Teaching and lesson-generation rules |

---

## Beginner Course Roadmap

| Module | Focus |
|---|---|
| 1 | ROS 2 environment, workspace, and package mechanics |
| 2 | First ROS 2 Python node |
| 3 | CLI inspection and `rqt_graph` visualization |
| 4 | Topics, publishers, subscribers, and bags |
| 5 | Services and clients |
| 6 | Custom messages and services |
| 7 | Parameters and YAML configuration |
| 8 | Launch files, remapping, and namespaces |
| 9 | Final beginner integration project |

Each module should end with something runnable, inspectable, and explainable.

---

## Teaching Style

Lessons in this repo should be:

- beginner-friendly
- hands-on
- low-storage aware
- written for ROS 2 Jazzy on Ubuntu 24.04
- clear about what each command does
- honest about common beginner mistakes
- focused on practical verification

Every lesson should include a small exercise or mini-project so learners can test their skills instead of only reading.

---

## Current Status

This repository is in active course-building mode.

The roadmap and installation guide are in place. Student-facing lessons will be created progressively from the roadmap, tested in a real ROS 2 environment, and expanded with troubleshooting notes as the course grows.

---

## For Course Authors

This repo includes Claude/Codex-oriented course authoring instructions:

- `AGENTS.md` tells coding agents how to work in this repository.
- `CLAUDE.md` defines the teaching quality bar.
- `.claude/commands/make-lesson-plan.md` defines `/make-lesson-plan <Lesson Number>`.
- `.claude/commands/make-lesson.md` defines `/make-lesson <Lesson Number>`.

Generated lesson plans should go in:

```text
Lessons/lesson-plan/
```

Generated student-facing lessons should go in:

```text
Lessons/lessons/
```

---

## Learning Philosophy

A small working ROS 2 system is better than a large confusing install.

Start with the core. Build one thing. Run it. Inspect it. Break it. Fix it. Then move to the next idea.

That is how this course is meant to be learned.
