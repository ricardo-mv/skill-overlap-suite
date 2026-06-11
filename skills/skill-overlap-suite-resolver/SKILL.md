---
name: skill-overlap-suite-resolver
description: Detects when two or more available skills overlap in topic or capability — either relative to a specific user task or across the full skill set — and helps the user decide which skill to use, in what order, or whether to combine them. Use this skill whenever a user asks "which skill should I use for X", "there seem to be two skills that do the same thing", "what's the difference between skill A and skill B", or when Claude itself detects that multiple skills are candidates for the same task. Also trigger proactively when the user's request clearly matches two or more available skills and choosing the wrong one (or ignoring one) would produce a suboptimal result. Do NOT skip this skill just because the overlap seems minor — surface it and let the user decide.
---

# Skill Overlap Resolver

Helps users navigate situations where two or more available skills cover the same topic or could apply to the same task. The goal is to orient the user — not to execute the task itself.

---

## When This Skill Triggers

Two modes:

### Mode A — Task-Driven (most common)
The user has a concrete task and Claude detects that 2+ skills are candidates.

Examples:
- "I want to write a LinkedIn post about our new product launch" → `social` + `launch` + `copywriting` all apply
- "Help me plan content for my restaurant's Instagram" → `social` + `content-strategy` + possibly a cooking/food skill
- "I need to audit my website" → `seo-audit` + `technical-seo` + `cro` all plausible

### Mode B — Explicit Overlap Question
The user asks directly about skill overlap or comparison, with or without a specific task in mind.

Examples:
- "What's the difference between `emails` and `sms`?"
- "Are `seo-audit` and `technical-seo` the same thing?"
- "I see both `content-strategy` and `marketing-plan` — which one do I need?"

---

## Resolution Process

### Step 1 — Understand the context
If the user hasn't provided a task, ask for one before proceeding. A task is the lens that makes the comparison meaningful. Even a brief description ("I want to grow my restaurant's social following") is enough.

### Step 2 — Identify candidate skills
Scan `available_skills` and filter by relevance to the task. List only the ones that genuinely apply — don't pad the list.

For each candidate, extract:
- What it does (from its description)
- What makes it distinct
- What it does NOT do (its boundaries)

### Step 3 — Map the overlaps
Identify specifically what overlaps:
- Same output type? (e.g., both produce email copy)
- Same trigger phrase? (e.g., both activate on "content calendar")
- Complementary steps in a sequence? (e.g., one plans, one executes)
- One is a subset of the other?

### Step 4 — Ask the user what output they prefer

Before presenting your analysis, ask:

> "¿Cómo prefieres que te presente esto?"
> - **Explicación clara** de en qué se diferencian
> - **Recomendación directa** ("usa esta")
> - **Comparación lado a lado**
> - **Árbol de decisión** para elegir según el caso

Then add, in the same message — without blocking on a response:

> "También puedo adaptar esta orientación a tu contexto específico si me cuentas más sobre el negocio o la audiencia — la recomendación podría cambiar."

This keeps the flow moving while opening the door to richer context. Do not wait for context before proceeding — only incorporate it if the user volunteers it.

(Adapt language to the user's — Spanish or English.)

### Step 5 — Deliver the chosen output format

The four formats are **not mutually exclusive** — they complement each other. A user may want more than one.

#### Explicación clara
Describe each skill's scope in plain language, highlight where they overlap, and explain what each covers that the other doesn't. Always include a practical "en la práctica" paragraph at the end showing the natural flow or sequence between skills — this is what turns a comparison into actionable guidance.

#### Recomendación directa
Give a single recommendation based on the user's task. If a combination is better, say so explicitly and explain the sequence (e.g., "start with A to plan, then use B to execute").

#### Comparación lado a lado
Use a table:

| Dimensión | Skill A | Skill B |
|---|---|---|
| Objetivo principal | … | … |
| Output típico | … | … |
| Cuándo es la mejor opción | … | … |
| Cuándo NO usarla | … | … |
| ¿Se pueden combinar? | Sí/No/Depende | — |

#### Árbol de decisión
Present a simple flowchart in text or Mermaid format:

```
¿Tu objetivo es planificar o ejecutar?
├── Planificar → usa skill A
└── Ejecutar
    ├── Canal email → usa skill B
    └── Canal social → usa skill C
```

### Step 6 — Offer to complement

After delivering the chosen format, always close with:

> "¿Quieres complementar esto con alguno de los otros formatos — [lista los que no se usaron aún]?"

This keeps the door open without overwhelming the user upfront. Let them pull more depth if they need it — don't push it all at once.

---

## Combination Guidance

When two skills are complementary rather than redundant, make the sequence explicit:

1. **Skill X first** — for [reason]
2. **Then Skill Y** — for [reason]
3. Shared inputs/outputs between them (what X produces that Y consumes)

If the skills are truly redundant (same output, same trigger, no meaningful difference for this task), say so clearly and recommend the more specific one.

---

## Edge Cases

- **Only one skill applies**: Say so briefly and suggest invoking it directly. Don't manufacture overlap.
- **No skill applies**: Flag this honestly. The task may be out of scope for the installed skill set.
- **More than 3 skills overlap**: Narrow the list first by asking the user to clarify their primary goal before presenting options.
- **Context changes the answer**: If the right choice depends on a detail the user hasn't shared (e.g., "is this for B2B or B2C?"), ask before recommending.

---

## Tone and Language

- Match the user's language (Spanish or English)
- Be direct — this skill exists to reduce confusion, not add to it
- Avoid jargon unless the user uses it first
- Keep recommendations actionable: end with a clear next step
