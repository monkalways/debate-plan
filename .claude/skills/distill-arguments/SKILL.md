---
name: distill-arguments
description: Distill reusable argument blocks from Lucas's graded practice-speech artifacts (daily-records/day-*.md) into a transferable knowledge bank, and enrich the shared mechanism/example banks. Use when the user wants to "distill/extract arguments" from a day file or day files, "build/update the knowledge bank" from practice speeches, harvest reusable mechanisms or examples from a transcript, or turn a scored motion into reusable cards. Format is World Schools (WSDC), Grade 8 level.
---

# Distill Arguments → Knowledge Bank

Turn a **motion artifact** (`daily-records/day-N.md` — motion + transcript + Yoodli + debate-coach score) into **reusable, transferable analysis** so an argument built for one motion is available the next time a similar topic is drawn.

## The design (why this exists)

Separate **reusable analysis** from **motion-specific packaging**. A bank organized by motion goes stale the moment an un-prepped motion is drawn (i.e. most of the time). So store transferable units as atoms and assemble motions on top of them. Three layers — **two already exist in this repo**:

| Layer | What | Where | Status |
|---|---|---|---|
| **1. Argument block** | one atomic argument = one warranted causal chain + its clash | `arguments/blocks/<topic>/<side>-<handle>.md` (one file per block, filed by topic) | **this skill builds it** |
| **2a. Mechanism library** | recurring causal moves (`A → B because C`) | `arguments/mechanism-bank.md` | exists — **enrich, don't duplicate** |
| **2b. Evidence/example bank** | a case/stat lives once, cited by many blocks | `arguments/examples-bank.md` | exists — **enrich, don't duplicate** |
| **2c. Framing/definitions** | frames, burdens, weighing standards | `reference/framing-and-style.md` | exists |
| **3. Motion files** | assembled per practice motion (disposable) | `daily-records/day-N.md`, `motions/worked-cases.md` | already the source |

The skill's job: **produce Layer 1, and link each block up to Layer 2** (never re-paste a mechanism or stat that already lives in a bank — link to it). When distillation surfaces a genuinely new mechanism or example, **append it to the relevant bank** (dedup first).

## Unfair advantage: these blocks come from GRADED speeches

Unlike a generic prep bank, every source here has a **debate-coach content score and a fix-by-fix verdict**. Use it: mark on each block whether the argument **actually landed** in the round or **flopped**, and preserve the coach's one-line reason. A block that scored the day's best (e.g. the moral-agency rights-denial that broke 7.75 on day-11·T2) is worth more than a block the judge quoted back against him (e.g. the "maybe we shouldn't use any animal" self-concede). Capture that signal in the `SOURCE` line.

## The argument block format

Template: `templates/argument-block.md`. One block = one causal chain, **each link warranted independently** so links can be swapped or attacked in isolation. The `THEY SAY → I SAY` block is what makes this training-grade rather than notes — you're storing the **clash**, not just the constructive.

Repo conventions to follow exactly:
- **Prop / Opp** (World Schools), not Gov/Opp.
- **`They say → I say`** (matches `mechanism-bank.md`), not "We say".
- **`[[wikilinks]]`** for backlinks (plain markdown — greppable now, Obsidian-openable later). Link to bank headings: `[[mechanism-bank#Harm Principle]]`, `[[examples-bank#COVID vaccines]]`, and `used in [[day-N]]`.
- **Tag vocabulary is the one already in use** — don't invent a parallel one:
  - `#type/*` from `motions/motion-taxonomy.md`: policy, abolition, value, regret, comparative, stance, actor, balance.
  - `#theme/*`: economics, society, politics, ethics, science (per CLAUDE.md).
  - `#mechanism/*` matches a `mechanism-bank.md` header family (harm-principle, deterrence, externality, …).
  - `#stakeholder/*`, `#principle/*` as relevant.
- **Filenames & foldering:** `arguments/blocks/<topic>/<side>-<kebab-handle>.md`. **File each block into the topic folder matching its primary `#theme` tag** — folders are `economics/`, `politics/`, `society/`, `ethics/`, `science-environment/`. E.g. `ethics/opp-human-life-ranks-first.md`, `politics/prop-16yo-are-stakeholders.md`. A motion's blocks may split across topic folders (the rights limb → `ethics/`, the practical limb → `science-environment/`); the `used in [[day-N]]` line + tags reassemble them by motion. Create a new topic folder only if a block genuinely fits none. Wikilinks are filename-based, so folder location never breaks `[[block-name]]` links.

## Procedure

1. **Scope.** Identify the target day file(s). Default = all `daily-records/day-*.md`. For a two-take file, prefer the **higher-scoring take** as the canonical version of a block, but note in `SOURCE` if an earlier take flopped (that failure is a `THEY SAY` waiting to happen).

2. **Read each artifact fully** — motion, transcript (both takes), Yoodli, and the `## Score (Content) — debate-coach` section. The score section already names what landed and what flopped; mine it.

3. **Extract distinct arguments.** One block per *constructive* argument (not per sentence). Rebuttal moves that recur (e.g. the "don't shut the hospital, raise the bar" reform-shield) become their own blocks too — they transfer. Skip motion-specific throwaways.

4. **Fill the block from the template.** Reconstruct the causal chain even if the speech delivered it loosely — the bank stores the *clean* version, warranted link-by-link. Pull the `THEY SAY` entries from: Yoodli's follow-up questions, the coach's "clash gap" notes, and the opponent lines the speech engaged.

5. **Link up, don't duplicate.** For each chain, check whether the mechanism already lives in `mechanism-bank.md` and the evidence in `examples-bank.md`. If yes → `LINKS` to it. If no and it's genuinely reusable → **append to the bank** (step 6). Never paste a full mechanism/stat into a block that a bank already holds.

6. **Enrich the banks (auto-append, dedup first).**
   - **Dedup:** grep the target bank for the concept before adding. A mechanism is a duplicate if its causal move matches an existing header's chain (even if worded differently); an example is a duplicate if the same case/stat already appears. If it's a *refinement* of an existing entry (e.g. a corrected stat — the day-11 Gallup "32% want equal animal rights" fixing a loose "90%"), **edit the existing entry**, don't add a second.
   - **Place it IN the right section, not a trailing "Distilled" block.** Insert each new mechanism under its matching theme header (`## ECONOMY`, `## RIGHTS`, `## SOCIETY & BEHAVIOUR`, …) and each new example under its domain header (`# Economics & Development`, `# Science, Tech & Environment`, `# Politics & Governance`, …), creating the theme/domain section only if none fits. For examples, also add a one-liner to that domain's **"Key facts to memorise"** footer. Do NOT append a separate batch at the end of the file — that creates duplicate theme sections. Mark distilled entries inline (mechanisms: a `(block: [[…]])` tag; examples: `✅ Verified` + a `Powers [[block]]` line) so provenance is visible without a separate section.
   - **Append format must match the bank's existing entries** (mechanism: 3-link `A → B because C` per side + weakest-link + They say→I say; example: fact / stat-or-case / "use it for" / weakest-link, tagged `theme · sub-theme · side`).
   - Preserve the banks' verify-before-you-cite discipline: round numbers, flag anything not confirmed. If a stat came from a transcript, WebSearch to confirm before banking it as fact (the examples bank is a fact source — don't poison it with a transcription artifact like "998.8%").

7. **Report.** End with a summary:
   ```
   ✅ N argument blocks written (list filenames)
   ✅ M mechanisms appended / K refined in mechanism-bank.md
   ✅ P examples appended / Q refined in examples-bank.md
   🏆 Best-scoring blocks (landed): ...
   ⚠️ Flopped/cautionary blocks (kept as anti-patterns): ...
   ```

## Guardrails

- **Grade the source's accuracy before banking a fact.** The coach log shows evidence was over-flagged twice — so don't auto-trust *or* auto-distrust a transcript stat. WebSearch to confirm, then bank the confirmed version. Note corrections in the block's `SOURCE`/`Evidence`.
- **Don't mutate `daily-records/day-*.md`** — those are the immutable source artifacts. This skill only writes to `arguments/blocks/` and appends to `arguments/*-bank.md`.
- **Tailor to Grade 8 / World Schools**, not university BP. Keep chains to 3 links, one warranted axis per weigh.
- **Blocks are scaffolds, not scripts** (same rule the banks carry) — a block that sounds memorised has been misused.
