# HOGWARTS_DAY

### A Reusable First-Person World-Experience Storytelling Workflow

**English** · [中文](README.zh-CN.md)

**让观众不只是观看一个世界，而是想要生活在其中。**

HOGWARTS_DAY is a reusable creative workflow for designing first-person world-experience stories and immersive short-form videos.

It explores how to transform the places, activities, routines, and emotional experiences of a fictional world into compelling audiovisual experiences that make audiences wish they could step inside that world.

---

## ✨ The Vision

What makes an audience fall in love with a fictional world?

Not just its spectacular landscapes, extraordinary creatures, or magical powers.

It is the feeling that there is a life waiting for them inside that world.

A place to visit.  
A routine to experience.  
A small discovery to remember.  
Someone to spend time with.  
A world they do not want to leave.

HOGWARTS_DAY is built around one central creative ambition:

> **Make the audience want to live in the world they have just watched.**

The goal is not simply to present a collection of beautiful shots. It is to design experiences that allow audiences to imagine themselves as participants rather than distant observers.

## 🎯 Core Experience Design

The project explores a four-stage audience journey:

**Recognition → Experience → Connection → Desire**

| Stage | Creative objective |
|---|---|
| Recognition | Introduce a world that feels distinctive and worth exploring. |
| Experience | Let the audience imagine participating in its everyday activities and extraordinary moments. |
| Connection | Build emotional attachment through routines, relationships, and small details. |
| Desire | Leave the audience wishing they could stay and experience more. |

Three creative dimensions support this journey:

- **World Wonders:** What makes the audience stop and stare?
- **Unique Experiences:** What makes the audience want to participate?
- **Life & Emotion:** What makes the audience want to stay?

## 🧭 The Workflow

HOGWARTS_DAY uses a staged creative workflow. Each stage has a defined responsibility and deliverable.

| Workflow | Responsibility |
|---|---|
| WF-00 · Project Initialization & Task Routing | Establish project context, constraints, and task ownership. |
| WF-01 · World-Life Research | Investigate the world's canon, everyday life, activities, locations, and experience opportunities. |
| WF-02 · Creative Planning | Develop the overall creative direction and experience strategy. |
| WF-03 · Scene Development | Design individual scenes through iterative creative review and approval. |
| WF-04 · Director Integration | Connect approved scenes into a coherent audiovisual experience. |
| WF-05 · Production & Review | Prepare production, evaluate results, and feed insights back into the workflow. |

### A Controlled Creative Process

The workflow emphasizes explicit decisions and stage boundaries:

- Research before creative planning.
- Audience experience before shot design.
- Develop, review, revise, and approve scenes individually.
- Preserve the distinction between verified source material and creative interpretation.
- Do not treat suggestions as approved decisions.
- Do not advance a stage without satisfying its required conditions.

The director retains final creative authority. AI agents assist with research, analysis, planning, documentation, and production tasks within explicitly defined boundaries.

## 🏗️ Architecture

The project separates reusable workflow rules from world-specific knowledge.

```text
HOGWARTS_DAY/
│
├── core/           # Reusable workflow foundations
├── world/          # World-specific knowledge
│   ├── canon/      # Canonical facts and source material
│   ├── experience/ # World experiences and research findings
│   └── references/ # Supporting references
│
├── planning/       # Creative planning
├── scenes/         # Individual scene development
├── director/       # Director-level integration
├── production/     # Production materials
├── reviews/        # Reviews and evaluations
├── assets/         # Approved reusable creative assets
│
├── AGENTS.md
├── PROJECT_RULES.md
├── PROJECT_STATE.md
├── WORKFLOW_SPEC.md
└── DECISION_LOG.md
```

The architecture is designed to keep two kinds of knowledge distinct:

**Reusable workflow knowledge**

Methods, procedures, decision rules, review standards, and collaboration protocols that can be reused across different fictional worlds.

**World-specific knowledge**

Canonical facts, locations, characters, activities, references, and approved experience designs belonging to a particular world.

This separation is intended to make the workflow adaptable beyond Hogwarts.

## 🤖 Human Direction, AI Collaboration

This project treats AI as a collaborative production system, not an autonomous creative authority.

The collaboration model is built on several principles:

- The human director defines the creative intent and makes final decisions.
- AI agents perform delegated tasks within explicit scopes.
- Research claims must retain traceable sources.
- Creative proposals must remain distinguishable from confirmed decisions.
- Approved experiences and reusable findings can be preserved as project assets.
- File modifications and Git operations require explicit authorization.

The project also maintains decision records and project-state documentation to reduce ambiguity across long-running creative sessions.

## 📍 Current Project Status

<sub>Version: v0.1 · Initial public baseline</sub>

The v0.1 baseline establishes the initial project structure, collaboration rules, and workflow specification.

Current development focuses on the first formal execution of WF-01: researching everyday life and experience opportunities within the Wizarding World.

| Area | Status |
|---|---|
| Initial project structure | Established |
| Core collaboration rules | Established |
| Workflow specification | Written |
| WF-00 | Conditional Pass |
| WF-01 | First formal research execution completed; fact corrections and director acceptance pending |
| WF-02 to WF-05 | Not started |
| Architecture validation through practical execution | In progress |

The workflow specification has been established, but its practical effectiveness has not yet been fully validated. This project is being developed iteratively.

## 🚀 Project Principles

1. **Experience over spectacle.** Visual spectacle matters, but it should serve a meaningful audience experience.
2. **Life over exposition.** Let audiences discover how a world works by experiencing it.
3. **Emotion over information.** Facts make a world understandable; emotional connections make it memorable.
4. **Research before invention.** Respect source material and clearly identify creative interpretations.
5. **Approval before progression.** Preserve explicit decision boundaries throughout development.
6. **Reusable knowledge over disposable output.** Turn approved discoveries into assets that can support future creative work.

## 🌍 Beyond Hogwarts

HOGWARTS_DAY begins with the Wizarding World as its initial creative environment.

However, the larger ambition is to develop a reusable method for creating first-person experiences across different fictional worlds.

A magical school.  
A futuristic city.  
A fantasy kingdom.  
A world that exists only in someone's imagination.

The underlying question remains the same:

**If the audience could enter this world for one day, what would make them wish they could stay forever?**

---

## English Summary

HOGWARTS_DAY is an experimental, reusable workflow for first-person world-experience storytelling.

It combines world research, audience-experience design, scene development, director-level integration, and production review into a structured human-AI collaboration process.

Its central ambition is to move beyond showing audiences what a fictional world looks like, and instead make them feel what it would be like to live there.

**The project starts with Hogwarts, but the workflow is designed to go further.**
