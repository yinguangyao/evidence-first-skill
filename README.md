# Evidence First Skill

Evidence First is a portable Codex skill for working in a Fable5-like mode: intent first, evidence before claims, conclusion first, and explicit verification before calling work done.

It is written in Chinese because the original workflow is optimized for Chinese collaboration, but the rules are model-agnostic and domain-agnostic. It works for research, debugging, analysis, writing, planning, and code delivery.

## What It Enforces

- Understand the user's real intent before executing literal wording.
- Attach evidence to every factual claim, number, path, command, or conclusion.
- Put the answer in the first sentence, then support it.
- Replace vague language with concrete evidence, numbers, examples, or explicit uncertainty.
- Never say tests passed or work is complete unless the verification actually ran.
- Always deliver with five fields: conclusion, premise check, verification, adjacent findings, and pending confirmations.

## Files

- `SKILL.md`: Codex skill entry point.
- `methodology.md`: Portable rules that can be pasted into another model's system prompt or first message.
- `phases.md`: Templates for splitting long work into clarify, scout, plan, execute, and deliver phases.
- `review.md`: Adversarial review prompt for a fresh context after producing the deliverable.

## Install In Codex

Clone or copy this directory into your Codex skills folder:

```bash
mkdir -p ~/.codex/skills
git clone git@github.com:yinguangyao/evidence-first-skill.git ~/.codex/skills/evidence-first
```

Then start a task that matches the skill description, or explicitly ask Codex to use `evidence-first`.

## Portable Use

For another model or agent:

1. Paste the full contents of `methodology.md` into the system prompt or first message.
2. Ask the model to expose scout findings and verification in the deliverable.
3. After it produces output, open a fresh context and paste `review.md` plus the output for adversarial review.
4. Treat every unsupported claim as pending confirmation.

## Maintenance Contract

The core rules are duplicated in `SKILL.md` and `methodology.md` so Codex gets the rules immediately while the portable version stays easy to copy. If you change any rule, update both files. `methodology.md` is the source of truth.
