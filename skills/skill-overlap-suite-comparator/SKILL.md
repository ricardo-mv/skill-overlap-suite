---
name: skill-overlap-suite-comparator
description: Produces a reusable reference document comparing two or more named skills in depth — their scope, boundaries, output types, ideal use cases, and how they relate to each other. Use this skill when the user wants to build a lasting reference guide about their skill stack, not just get oriented for a single task. Trigger when the user says things like "document the difference between A and B", "create a comparison guide for my skills", "I want a reference I can consult later", "map out how these skills relate", or "build a skill reference sheet". Distinct from skill-overlap-resolver (which orients in the moment) — this skill produces a document the user can save, share, or consult repeatedly. Also trigger when the user has already used skill-overlap-resolver and wants to formalize the output into a permanent reference.
---

# Skill Comparator

Produces a structured, reusable reference document comparing two or more skills. The output is meant to be saved and consulted repeatedly — not just read once and forgotten.

---

## When This Skill Triggers

- User names two or more skills and wants a formal comparison document
- User wants to map their full skill stack or a subset of it
- User has already used `skill-overlap-resolver` and wants to formalize the output
- User wants a reference guide to share with a team or collaborator

---

## Process

### Step 1 — Identify the skills to compare
If the user named specific skills, use those. If the request is broader ("compare all my SEO skills"), scan `available_skills` and group by topic area, then confirm the scope with the user before proceeding.

### Step 2 — Ask for document scope
Before writing, confirm:
- **How many skills** are being compared? (2–3 is a focused doc; 4+ becomes a reference index)
- **What's the primary use case** for this document? (personal reference, team onboarding, deciding which to install/remove)
- **Format preference**: comparison table, narrative guide, or both

### Step 3 — Build the comparison document

#### For 2–3 skills: Full comparison
Produce a document with these sections:

**Overview**
One paragraph per skill explaining what it does in plain language — written as if the reader has never seen it before.

**Where they overlap**
Specific list of what both/all skills share: same trigger phrases, similar outputs, shared use cases.

**Where they differ**
The key distinctions — what each skill does that the others don't. This is the most important section.

**When to use each**
Concrete scenarios for each skill. Use real examples when possible (draw from user context if available).

**How they can work together**
If the skills are complementary, describe the natural sequence. What does Skill A produce that Skill B consumes? What's the handoff point?

**Quick reference card**
A summary table at the end:

| | Skill A | Skill B | Skill C |
|---|---|---|---|
| Primary question answered | … | … | … |
| Typical output | … | … | … |
| Best used when | … | … | … |
| Not the right choice when | … | … | … |
| Combines well with | … | … | … |

#### For 4+ skills: Reference index
When comparing many skills at once, produce an index format:
- Group skills by function (planning, execution, analysis, etc.)
- For each group, note the primary skill and when to reach for alternatives
- Include a master table covering all skills

### Step 4 — Deliver and offer formats

After delivering the document, ask:
> "¿Quieres que lo exporte como archivo Markdown para guardar, o con este formato en el chat es suficiente?"

If the user wants a file, save it as a Markdown file named `skill-comparison-[topic].md` in the current environment's output/working directory (the user's selected folder in Cowork, the outputs folder on claude.ai, or the working directory in Claude Code) and present it.

---

## Output Principles

- Write for a reader who will come back to this document weeks later — no assumed context
- Prioritize the **differences** over the similarities — that's what makes the doc useful
- Use the user's actual skill names exactly as installed (don't rename or abbreviate)
- If context about the user's work is available (from memory or project files), use real examples — not generic ones
- Keep the quick reference card always — it's the part users return to most

---

## Edge Cases

- **Skills are truly redundant**: Say so explicitly. Recommend which one to keep and suggest removing the other.
- **User names a skill that isn't installed**: Flag it and offer to compare based on the skill's public description if available.
- **More than 6 skills**: Suggest splitting into multiple focused documents by topic area rather than one overwhelming comparison.
