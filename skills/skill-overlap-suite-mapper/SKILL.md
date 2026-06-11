---
name: skill-overlap-suite-mapper
description: Proactively maps skill overlaps relevant to the user's specific context — their work, projects, and industry — without needing a concrete task as a trigger. Uses available context (Claude memory in claude.ai, project files in Projects, CLAUDE.md in Claude Code, workspace files in Cowork) to identify which overlaps actually matter for this user. Trigger when the user says "map out my skills for my context", "which overlaps should I know about given what I do", "give me a proactive skills overview", "what overlaps are relevant for my business", or "analyze my skills given my projects". Also trigger when the user wants a strategic view of their skill stack before starting work. Distinct from skill-overlap-resolver (reactive to a task) and skill-comparator (documents specific pairs) — this skill maps the full picture through the lens of who the user is.
---

# Skill Overlap Mapper

Produces a personalized map of skill overlaps that are relevant to the user's specific context. Instead of analyzing all possible overlaps generically, it filters through the lens of what the user actually does — making the output actionable rather than exhaustive.

---

## When This Skill Triggers

- User wants a strategic overview of their skill stack before starting a project
- User has just installed a new set of skills and wants to understand how they fit together
- User asks proactively about overlaps without a specific task in mind
- User wants to know which overlaps they're likely to encounter given their work

---

## Context Sources by Environment

This skill adapts to whatever context is available:

| Environment | Context source |
|---|---|
| **claude.ai** | Claude memory — past conversations, user profile, known projects and industries |
| **Claude Projects** | Project documents, instructions, and files uploaded to the project |
| **Claude Code** | `CLAUDE.md`, codebase structure, README files |
| **Cowork** | Workspace files, project briefs, any documents in the session |

Always declare at the start what context source you're using, so the user knows the basis for the analysis.

---

## Process

### Step 1 — Declare context and confirm scope

Open with a brief statement of what context you have available, for example:

> "Basándome en lo que sé de tu trabajo — dos empresas (Anfibio TGR y Menval), con foco en gestión de residuos y comercialización médica — voy a mapear los solapamientos de skills que tienen más probabilidad de aparecerte."

Then ask one scoping question before proceeding:
> "¿Quieres que me enfoque en algún área en particular (marketing, operaciones, contenido...) o prefieres una vista completa?"

### Step 2 — Filter skills by relevance to user context

Scan `available_skills` and discard skills that have no plausible connection to the user's work. Do not include skills just because they're installed — only include those where the user's context makes them likely to be used.

Group the relevant skills into functional clusters, for example:
- Contenido y marketing digital
- SEO y presencia web
- Campañas y comunicación
- Estrategia y planificación
- Operaciones y procesos

### Step 3 — Identify overlaps within each cluster

For each cluster, identify which skills share triggers, outputs, or use cases. Be specific:
- What exact phrase or task would make both skills fire?
- What would the user lose by choosing one over the other?
- Is the overlap a conflict (use one OR the other) or a sequence (use one THEN the other)?

### Step 4 — Produce the overlap map

Structure the output as a **personalized reference map**:

---

**[Cluster name]**

Skills in this cluster: `skill-a`, `skill-b`, `skill-c`

Overlap: `skill-a` and `skill-b` both activate when you want to [specific trigger]. The difference is that `skill-a` [what it does uniquely] while `skill-b` [what it does uniquely].

Recommended default for your context: `skill-a` — because [reason tied to user's specific work].

When to reach for `skill-b` instead: [specific scenario].

---

Repeat for each cluster that has meaningful overlaps. Skip clusters with no overlap — note them briefly as "sin solapamientos relevantes en este grupo."

### Step 5 — Produce a master decision guide

At the end of the map, include a condensed reference:

**Guía rápida de decisión para [user's context]**

| Si quieres... | Usa primero | Considera también |
|---|---|---|
| [common task 1] | skill-x | skill-y si [condition] |
| [common task 2] | skill-a | skill-b para [specific case] |
| … | … | … |

This table should reflect the user's actual recurring tasks — not generic examples.

### Step 6 — Offer next steps

Close with:
> "¿Quieres que profundice en algún cluster específico, o que exporte este mapa como documento de referencia?"

If the user wants a file, save it as a Markdown file named `skill-overlap-map-[date].md` in the current environment's output/working directory (the user's selected folder in Cowork, the outputs folder on claude.ai, or the working directory in Claude Code) and present it.

---

## Output Principles

- **Personalization over exhaustiveness** — a map with 5 relevant overlaps is more useful than one with 20 generic ones
- **Always tie recommendations to the user's context** — "para tu caso" not "en general"
- **Sequences over conflicts** — when skills can work together, show the flow; don't just say "use one or the other"
- **Declare your context source** — the user should know if the analysis is based on memory, project files, or assumptions
- **Update on request** — if the user adds context mid-session, regenerate the relevant sections

---

## Edge Cases

- **No context available**: If Claude has no memory or project files to draw from, ask 3 targeted questions before proceeding: industry/domain, primary use cases for skills, team size. Don't produce a generic map — it defeats the purpose of this skill.
- **Too many installed skills**: If there are 50+ skills, focus the map on the top 3–4 clusters most relevant to the user. Offer to expand.
- **User's context has changed**: If memory or project files seem outdated, flag it: "Esto está basado en lo que sé de ti — si algo ha cambiado, cuéntame y ajusto el mapa."
