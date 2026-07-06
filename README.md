# proof-gate

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An adversarial build-and-verify loop for high-stakes delivery work — releases, migrations, security or compliance changes, anything where a confident-but-wrong "done" claim is expensive. It's for anyone directing AI agents (or a human team) through work that needs to be *proven* correct, not just plausible.

Proof-gate exists because "it looks done" and "it is proven done" are two different claims, and a lot of verification is theater: checks that pass because they can never fail, self-reported metrics, a happy-path test standing in for the real thing. This skill is a discipline for closing that gap.

## The core loop

1. **Build** — a builder produces the change.
2. **Independent adversarial verify** — a separate reviewer, in a fresh context, is told to *refute* the claim rather than confirm it. It re-derives all evidence itself and never trusts the builder's notes.
3. **Fix-loop** — findings go back to the builder until the claim is clean or an honest blocker is declared.
4. **Gated merge** — nothing merges until the real proof bar is met, not just a green check.

Full detail — the honesty contract, the real-proof-bar table by domain, the cleanroom release checklist, and the mutation-test self-check for verifiers — lives in [SKILL.md](SKILL.md).

## Model-agnostic, tool-agnostic

Nothing here is Claude-specific. `SKILL.md` is a plain markdown file with a YAML frontmatter header and a body. Use it however fits your setup:

- **As a Claude Code skill**: drop the `proof-gate` directory into your skills folder (or wherever your Claude Code setup loads skills from) so it can be invoked by name or triggered by its description.
- **As a system-prompt block for any other agent** (Codex, a custom agent, etc.): copy everything in `SKILL.md` below the `---` frontmatter and paste it into that agent's system prompt or `AGENTS.md`. It reads as a self-contained set of instructions either way.

## When to use it — and when not to

Use it for releases, migrations, security/compliance changes, or any work where a wrong "done" claim is costly, especially when coordinating a lean coordinator model against cheaper worker/builder models and independent verifiers.

Skip it for trivial edits, cosmetic changes, and throwaway prototypes — the overhead only pays for itself when being wrong is expensive.

## License

MIT — see [LICENSE](LICENSE).
