---
name: llm-council
description: Convene a 3-model council (Claude + GPT via codex CLI + Gemini CLI) on a high-stakes decision. Forces cross-critique between members and surfaces where they actually disagree, breaking Claude's default agreeableness. Use when the user asks to "convene a council", "get a second opinion", "ask GPT and Gemini", "what would other models say", or has an architecture / strategy / hiring / pricing decision where being wrong is expensive. Skip for factual questions, code with one right answer, or anything premortem-shaped (route to premortem skill instead).
allowed-tools: Read, Glob, Grep, Write, Bash
---

# LLM Council

Three frontier models, one decision. Output is **not** three answers side-by-side — it's a structured map of agreement, disagreement, and which disagreements matter for this user's call.

## Members

| Member | Invocation | Bias to expect |
|---|---|---|
| Claude (this session) | direct reasoning | Pragmatic, agreeable, code-rooted |
| GPT-5.5 | `codex exec` | Skeptical, hedge-prone, edge-case sensitive |
| Gemini | `gemini -p` | Structural, taxonomical, categorization-heavy |

## When to run

**Good fit:**
- Architecture/design with long-lived consequences
- Strategy calls (pricing, positioning, hiring) where Claude's agreeableness is a real risk
- "Am I thinking about this right?" — challenge the framing, not the plan
- Any decision the user explicitly flags as high-stakes

**Bad fit:**
- Factual lookups
- Code with one right answer
- Premortem-shaped questions ("what could go wrong") — route to `premortem`
- Speed > depth

## CLI invocations (verified)

**Codex (GPT-5.5):**
```bash
TMPF=$(mktemp)
codex exec --skip-git-repo-check -o "$TMPF" "<prompt>"
ANSWER=$(cat "$TMPF") && rm "$TMPF"
```
- `--skip-git-repo-check` is required outside trusted dirs
- `-o <file>` writes just the final message (avoids verbose preamble in stdout)

**Gemini:**
```bash
gemini -p "<prompt>"
```
- Outputs the answer directly to stdout
- Add `-m <model>` to pin a model

**Run in parallel** via two simultaneous Bash tool calls in a single message. Don't sequence them.

## Process (3 rounds)

### Round 1 — Independent answers

Send the question to all three members in parallel. None see the others' answers.

Each member gets the same prompt: the user's question + relevant context + this directive:

> "Answer in under 250 words. Be direct. State your strongest position, not a hedged one. End with the single biggest risk you see in your own answer."

The "biggest risk in your own answer" line is load-bearing — it primes the model to flag its own weakness, which makes round 2 more productive.

### Round 2 — Cross-critique (anonymized)

Send each member the other two answers, **with peer identities anonymized as "Model A" and "Model B"**. Each model gets a different random A/B mapping so it can't infer who's who across runs. The model never learns which family produced which answer.

Why anonymize: prevents brand bias — deferring to known-strong models, attacking known-weak ones, or refusing to disagree with one's own family. Without this, R2 critiques drift toward politics instead of substance. Credit: Karpathy's [llm-council](https://github.com/karpathy/llm-council).

Prompt:

> "Two other models answered the same question. Their identities are anonymized.
>
> Model A: ...
> Model B: ...
>
> Where are they wrong? Where are they right and your original answer was wrong? Be specific. Don't be polite. Under 200 words."

In the transcript, record the anonymization mapping so you can de-anonymize for the synthesis step. The user-facing report uses real names; only the cross-critique itself is blind.

This is the round that produces the value. Without it the skill is theatre.

### Round 3 — Synthesis (Claude, this session)

Read all 6 outputs (3 answers + 3 critiques) and produce:

1. **Where the council agrees** — 1-3 points. If they all converge, say so plainly. Do not manufacture disagreement.
2. **Where the council disagrees** — the actual deltas. Each side's strongest argument in 1-2 sentences.
3. **Which disagreement matters most** — for this user's specific decision, which delta should drive the call?
4. **Recommendation** — Claude's call. Explicitly name which member you're siding with on the load-bearing disagreement and why.

**Self-bias check** (mandatory before finalizing): Claude is both a member (R1 answer) and the chairman (this synthesis). That's a structural conflict — Claude will systematically over-weight its own R1 because (a) it has session context the others lack, and (b) it "feels right" to itself. Before finalizing the recommendation, ask: *am I siding with my own R1 answer because it's actually better, or because I wrote it?* If the only reason it's winning is "I have more context," that's not a real reason — GPT and Gemini may have caught a blind spot Claude doesn't see. State the bias check explicitly in the synthesis output (one sentence) so the user can audit it.

## Output

**Chat:** the 4-section synthesis. Concise. End with a clear recommendation.

**File** (only if the question is consequential or the user asks): `council-YYYYMMDD-HHMMSS.md` in CWD with full transcript — the question, R1 answers, R2 critiques, R3 synthesis. Use `date +%Y%m%d-%H%M%S` for the timestamp.

## Context passing

The cold CLIs don't see this conversation. The skill must build a self-contained prompt for each member:

1. The question itself
2. Relevant context the user has shared (paste relevant excerpts, don't reference "the file we discussed")
3. Specific constraints (budget, timeline, audience, existing tech) — explicit, not assumed
4. Cap each round's response length so synthesis stays tractable (250 words R1, 200 R2)

If the question depends on a file or codebase, paste the relevant excerpts directly into the prompt. Don't assume the CLI agents can see the workspace.

## Failure handling

- **One CLI fails:** proceed with two members. Note the missing voice in synthesis. Don't retry more than once.
- **All three converge:** say so plainly. "The council agrees on X. Recommendation: do X." Manufactured drama is worse than agreement.
- **Council disagrees with the user's framing entirely:** flag this explicitly. Sometimes the right output is "all three models think you're solving the wrong problem."
- **Timeout:** wrap each call in a 90s timeout. Members are independent; one slow call shouldn't block synthesis.

## Anti-patterns

- Showing raw R1/R2 output without synthesis — the synthesis is the product
- Weighting all three equally on every topic — Claude has session context, the others don't. Weight accordingly
- Burying the recommendation in hedged language — end with a clear call
- Running the council on simple questions — hard-gate this skill
- Skipping R2 to save tokens — R2 is the value; without it just ask Claude

## Compose with premortem

If the council's recommendation is a concrete plan with steps (not just a yes/no or a framing), end with one line: "Want me to run a premortem on this plan to surface failure modes before you commit?" Skip if the recommendation is reversible/cheap or the user signaled closure.

## Smoke test

Before using on a real decision, verify both CLIs work:

```bash
gemini -p "say hi in 5 words"
codex exec --skip-git-repo-check -o /tmp/codex-test "say hi in 5 words" && cat /tmp/codex-test
```

Both should return one short sentence.
