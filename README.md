# HOGWARTS_DAY

### An agent workflow for research-driven, first-person world-experience video creation

**English** · [中文](README.zh-CN.md)

**Make the audience not just watch a world — but want to live in it.**

HOGWARTS_DAY is a creative workflow project built for AIGC video production. Its goal is not simply to generate video, but to establish a reusable pipeline that runs from **world research → episode-level creative planning → scene and shot direction → video-generation prompt assembly**.

Although HOGWARTS_DAY is currently the practice project (set in the Wizarding World), it is designed to be **adaptable across genres and projects** — not a prompt repository for making Hogwarts videos only.

> Honest scope: the cross-project architecture has a foundation, but it has **not yet been validated end-to-end across different subject matter**. The v0.1 workflow is in active development; see [Current Status](#-current-status) for exactly what is and is not verified.

---

## ✨ Vision

What makes an audience fall in love with a fictional world?

Not just spectacular landscapes, extraordinary creatures, or magical power — but the feeling that there is a life waiting for them inside that world.

A place to visit. A routine to experience. A small discovery to remember. Someone to spend time with. A world they do not want to leave.

The project is built around one creative ambition:

> **Make the audience want to live in the world they have just watched.**

The four-stage audience journey that organizes all creative work:

**Recognition → Experience → Connection → Desire**

| Stage | Creative objective |
|---|---|
| Recognition | Introduce a world that feels distinctive and worth exploring. |
| Experience | Let the audience imagine joining its everyday activities and extraordinary moments. |
| Connection | Build emotional attachment through routines, relationships, and small details. |
| Desire | Leave the audience wishing they could stay and experience more. |

The pipeline moves from **world research** to **audience-experience design** to **video generation**: understand the world, decide what the audience should experience, then produce the prompts that realize it on screen.

---

## 🧭 Workflow Overview

The project organizes creative work into long-horizon workflows. The three currently defined are:

| Workflow | Responsibility | Definition status |
|---|---|---|
| **WF-01 · World Research** | Research the world, setting, locations, daily life, experiences, and raw material usable for video creation. Produces world knowledge and candidate experiences. | Research practice done; formal spec not yet consolidated into the repo (see status) |
| **WF-02 · Episode Creative Planning** | Turn an idea seed into a complete episode director's script through a seven-stage process. | Closed after first real end-to-end run (V0.2.1) |
| **WF-03 · Director Script → Video-Generation Prompt Assembly** | Convert a WF-02 director script into executable video-generation prompts, per director-specified scope and strategy. | Definition v1.1 approved; first real processing done; long-term stability unverified |

> WF-04 (global director integration) and WF-05 (production & review) are specified at a high level in `WORKFLOW_SPEC.md` but **not yet started**.

Detailed definitions live in **`WORKFLOW_SPEC.md`** (WF-00~WF-05) and **`core/WF-03-导演稿到视频提示词加工工作流-v1.0.md`** (authoritative WF-03 spec). The README summarizes; the specs are the source of truth.

### WF-01 · World Research

Researches the creative subject's world: canon, setting, locations, ways of life, experiences, and usable material. The core objective is to **supply world knowledge and candidate experiences** for downstream planning.

Output: world research documents with source/credibility annotations, plus a **candidate-experience list** (candidates are marked and are not treated as approved until the director accepts them).

> Note: WF-01 has completed a first formal practice run, but **that specific research report is not part of this workflow commit** and remains pending fact-correction and director acceptance. No consolidated formal WF-01 spec has been written into the repository yet.

### WF-02 · Episode Creative Planning

Turns an idea seed into a complete episode-level director's script. Its seven-stage process:

1. **Idea intake & task definition**
2. **Idea development & experience selection**
3. **Episode experience composition & structure design**
4. **Audience attention & experience-delivery review**
5. **SC scene planning**
6. **SH shot-level director design**
7. **Episode integration, quality check & delivery**

**Agent architecture:**

- **One lead Agent** handles overall planning, orchestration, integration, and final delivery.
- Specialist roles contribute on demand: **M1** idea generation, **M2** experience evaluation, **M3** structure design, **M4** attention design.
- Specialist agents are **invoked as needed, not a mandatory parallel pipeline**.
- The **director retains key creative decisions and approval authority.**

**SC vs SH:**

- **SC (scene unit)** — a scene unit of the episode.
- **SH (shot design unit)** — a shot-level design unit.
- **SH is not a video-generation clip.** One SH may be split into multiple generation tasks.

### WF-03 · Director Script → Video-Generation Prompt Assembly

Converts a WF-02 director's script into executable prompts. Key properties:

- **SC is the basic unit of processing**, but the director may specify a whole SC, a single SH, multiple SHs, or a specific generation task.
- **One lead Agent independently completes the specified task.**
- Each task actually reads the **final WF-02 director's script**, the **ACTING skill**, and the **CINEDANCE skill**.
- **ACTING** handles observable character performance where applicable (on-screen characters only; never invent performance in pure-POV/no-character shots).
- **CINEDANCE** handles space, first frame, optics, camera, physics, lighting, continuity, prompt assembly, and QA.
- Supports **text-only T2V, reference images, first/last frames, multi-reference, or mixed strategies**, per the director's instructions.
- Delivers **complete executable prompts, generation-task mapping, reference-asset manifest, and QA results**.

WF-03 **does not redesign the director's intent** and does not change the director-specified generation strategy.

---

## 🤖 Agent Architecture & DSH

The project uses **DSH (DeepSeek Harness)** as its current execution environment. The workflows are designed around a **lead Agent** that routes and integrates work, with specialist sub-agents and skills called on demand — not a fixed parallel pipeline.

**Two reusable skills are shipped with the repository** (under `.dsh/skills/`) and are WF-03's execution dependency:

| Skill | Role |
|---|---|
| `acting` | The character-acting layer of video prompts: objectives, beats, tactics, subtext, body/status, eye life, voice. |
| `cinedance-higgsfield` | Cinematic prompt direction for Seedance 2.0 / Higgsfield: scene context, spatial blocking, first frame, optics/FOV, camera, timing, physics, lighting, audio, continuity, reference control, and final prompt assembly. |

> `.gitignore` uses **precise exceptions**: it tracks only these two named skills, not the whole `.dsh/` local runtime environment. The rest of `.dsh/` stays local and private.

The workflow assets are **not tied to DSH** — the rules are written as portable documents. Migrating or adapting to another agent environment is possible in principle but **has not been verified**.

---

## 📂 Project Organization

The repository separates **reusable workflow assets** from **project-specific instances**.

### Reusable workflow assets

- **`core/`** — reusable workflow definitions (e.g. the WF-03 spec).
- **`planning/WF-02/`** — reusable WF-02 research methods and knowledge assets (M1–M4).
- **`.dsh/skills/`** — the two reusable skills (`acting`, `cinedance-higgsfield`).
- **Root rules & entry documents** — `AGENTS.md`, `PROJECT_RULES.md`, `WORKFLOW_SPEC.md`, `DECISION_LOG.md`, `PROJECT_STATE.md`.

### Project-specific instances

- **`planning/EPxx/`** — a specific episode's creative brief, director's script, scene plan, etc.
- **`production/EPxx/`** — a specific episode's prompts, reference material, and video outputs.

An episode's creative content, director's script, generation prompts, reference assets, and video products are managed **separately** from the general workflow assets. Reusable methods live in `core/` and `planning/WF-02/`; a particular episode's material lives in `planning/EPxx/` and `production/EPxx/`.

> Note: not all of a given episode's material is necessarily committed to Git. General workflow assets and project-specific instances are managed under distinct boundaries, and large production outputs (video, renders, image assets) are excluded by `.gitignore`.

```text
HOGWARTS_DAY/
├── core/            # Reusable workflow definitions
├── planning/
│   ├── WF-02/       # Reusable WF-02 research methods & knowledge (M1–M4)
│   └── EPxx/        # Episode-specific planning (brief, script, SC plan, …)
├── production/
│   └── EPxx/        # Episode-specific prompts, references, outputs
├── world/           # World research knowledge (canon / experience / references)
├── scenes/          # Per-scene development
├── director/        # Director-level integration
├── reviews/         # Reviews & retrospectives
├── assets/          # Approved reusable creative assets (index)
├── .dsh/skills/     # The two reusable skills
├── AGENTS.md
├── PROJECT_RULES.md
├── PROJECT_STATE.md
├── WORKFLOW_SPEC.md
└── DECISION_LOG.md
```

---

## 🚀 Quick Start

1. **Get the repository.**
   ```bash
   git clone https://github.com/doublezzz0409/HOGWARTS_DAY.git
   cd HOGWARTS_DAY
   ```
2. **Confirm a DSH environment.** The workflows assume DSH as the current execution harness.
3. **Confirm project rules are loaded.** `AGENTS.md` is the entry point and references `PROJECT_RULES.md` (full rules) and `DECISION_LOG.md` (director decisions).
4. **Confirm the two skills are discoverable by name** from `.dsh/skills/acting/` and `.dsh/skills/cinedance-higgsfield/`.
5. **Prepare an isolated project directory and project context** (e.g. `planning/EPxx/`, `production/EPxx/` for a new episode).
6. **Invoke the appropriate workflow** for the task at hand:
   - World/setting/life-experience questions → **WF-01**
   - "What is this episode about?" → **WF-02**
   - "Turn the director's script into video-generation prompts" → **WF-03**

> This is a work-in-progress creative workflow, not packaged software. There are **no one-click installers or automation scripts**; some setup (DSH environment, skill registration, project context) is **manual**.

---

## 📍 Current Status

<sub>Baseline: v0.1 · working draft under active development</sub>

| Area | Status |
|---|---|
| **WF-01 · World Research** | First real practice research completed; the specific report is **not included in this workflow commit**; pending fact-correction and director acceptance. |
| **WF-02 · Episode Creative Planning** | **V0.2.1 first real end-to-end run complete; formally closed.** |
| — M1 · Idea generation | Reference-level stage results; **not formally accepted**. |
| — M2 · Experience value & selection | v1.0 complete; **pending director acceptance** (results still marked candidate). |
| — M3 · Experience composition & structure | v1.0 **formally accepted by the director**. |
| — M4 · Audience attention & delivery | v1.0 **formally accepted by the director**. |
| — M5 · Production constraints & QA | **Deferred** (director will evaluate personally). |
| — M6 · Integration, case validation & method transfer | **Deferred**. |
| **WF-03 · Prompt assembly** | Definition **v1.1 approved**; EP01 SC03 completed a **first real processing run**; **long-term stability and cross-project reuse not yet verified**. |
| **WF-04 · Global director integration** | Not started. |
| **WF-05 · Production & review** | Not started. |

> Important: research-level findings are candidate conclusions and have **not been empirically validated with real audience data**. A single successful run does **not** mean long-term stability is proven. Nothing here is described as audience-proven fact.

---

## ⚠️ Limitations & Roadmap

**What is not yet verified:**

- **No real audience data.** Retention, psychology, and "does the audience actually want to live in this world" are not measured. Attention findings rest on third-party structure analysis, not platform backend metrics.
- **Cross-project reuse is unproven.** The architecture is designed to generalize beyond Hogwarts, but has not been validated on a different subject with a full real production.
- **Long-term stability of WF-03 is unverified.** One real processing run (EP01 SC03) is not proof of sustained reliability.
- **Reference assets are largely absent.** Character/location/prop reference images and a character profile/voice library do not yet exist, so reference-based (R2V) identity consistency cannot yet be truly executed.
- **Fact status is not fully settled.** Some WF-01 canon facts and a continuity item remain pending; downstream prompts must carry those flags, not treat them as confirmed.
- **M5/M6 deferred**, so production feasibility, continuity/cost risk, and whole-episode quality currently depend on the director's manual judgment.
- **Not tied to one agent framework.** Besides DSH, portability to other agent environments is a stated goal, not a tested fact.

**Toward validation:** the intended next step is to move from research toward **practical, creation-driven validation** — using M2/M3/M4 to plan a minimal sample, then learning from real generation and review. This validates the design logic; it does **not** substitute for audience data.

---

## 📜 Project Principles

1. **Experience over spectacle.** Visual spectacle serves a meaningful audience experience.
2. **Life over exposition.** Let audiences discover how a world works by experiencing it.
3. **Emotion over information.** Facts make a world understandable; emotional connection makes it memorable.
4. **Research before invention.** Respect source material; clearly mark creative interpretation.
5. **Approval before progression.** Explicit decision boundaries; the director holds final creative authority.
6. **Reusable knowledge over disposable output.** Turn approved discoveries into reusable workflow assets.

For the full rules, see [`PROJECT_RULES.md`](PROJECT_RULES.md). For the six workflows' inputs/tasks/outputs, see [`WORKFLOW_SPEC.md`](WORKFLOW_SPEC.md). For director decisions, see [`DECISION_LOG.md`](DECISION_LOG.md). For live project state, see [`PROJECT_STATE.md`](PROJECT_STATE.md).

---

## 🌍 Beyond Hogwarts

HOGWARTS_DAY begins with the Wizarding World as its first creative environment, but the larger ambition is a **reusable method for first-person world-experience video creation across different fictional worlds**.

A magical school. A futuristic city. A fantasy kingdom. A world that exists only in imagination.

The underlying question stays the same:

**If the audience could enter this world for one day, what would make them wish they could stay forever?**
