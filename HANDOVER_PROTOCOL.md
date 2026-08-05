# HANDOVER_PROTOCOL.md
## Stage-Gate Handover & Cohesion Protocol

> **FILE ROLE:** Operating instructions for moving between stages and maintaining cohesion across chats. Machine-readable. Read when closing out a stage or starting a new one.
> **LOCATION:** GitHub repo (reference) + a copy of the *current* handover manifest is what gets attached/pasted into the new chat.
> **WHY THIS EXISTS:** Modular files risk Stage 5 forgetting a dependency locked in Stage 2. This protocol carries the structural weight of each completed stage forward without forcing the model to re-read every full stage document.

---

## 1. CLOSING OUT A STAGE (run in the *current* chat, before opening a new one)

When a stage is complete (all six quality gates passed — see 00_GLOBAL_INDEX.md §4), run this in the active chat:

> *"I am closing out Stage [N]. Analyse our progress against 00_GLOBAL_INDEX.md. Generate a 5-bullet Handover Manifest containing: (1) core decisions locked in this stage, (2) active variables / dependencies inherited by the next stage, (3) constraints this places on downstream stages, (4) any unresolved items carried forward, (5) the recommended starting point for the next stage."*

The agent produces the manifest. **You (the founder) approve it** before proceeding.

---

## 2. THE UPSTREAM UPDATE (the cohesion mechanism)

After approval, take the 5-bullet manifest and **append it to §6 (Cumulative Handover Log) of 00_GLOBAL_INDEX.md** in the Ninja project folder, under the matching stage heading.

Why this matters: because 00_GLOBAL_INDEX.md is read as background context in *every* new chat in the project, the AI now carries the structural weight of the completed stage forward automatically — **without needing to read the full stage document**. This is the single most important token-saving + cohesion mechanism in the whole architecture.

> **Maintenance rule:** If §6 exceeds ~600 words, migrate settled bullets into the relevant stage file on GitHub and leave a one-line pointer in §6. Never let the Global Index bloat past its token budget.

---

## 3. ALSO AT CLOSE-OUT: push the stage file to GitHub

- Save the completed stage's Master .md (and .pdf) to the GitHub repo.
- Update the Status column in 00_GLOBAL_INDEX.md §3 (☐ → ◐ → ☑).
- Record version + date in the stage file's own §6 (Version History).

---

## 4. STARTING A NEW STAGE (in a *new* chat)

Do **not** start a new stage by re-explaining the project. Do this instead:

1. Open a new chat **inside the Ninja project folder** `Intellectual Enterprise Guidelines (Master Document)`. (This auto-loads 00_GLOBAL_INDEX.md + 00_DIGITAL_TWIN_CORE.md as background — no need to attach them.)
2. Paste or attach **only the handover manifest** for the stage you're about to begin (from §6 of the Global Index, or the manifest the previous chat produced).
3. Send a single starting instruction:

> *"Read the project background (00_GLOBAL_INDEX.md and 00_DIGITAL_TWIN_CORE.md are in this project's files). I am beginning Stage [N] — [stage name]. The handover manifest is attached/pasted below. Fetch the stage file `0[N]_STAGE_[NAME].md` from the GitHub repo `intellectual-enterprise-guidelines` and confirm you have: the global rules, the cumulative handover log, the founder identity, and this stage's scope. Then propose the first step."*

4. The agent confirms ingestion and proposes a first step. You approve, then work begins.

**Why this works:** The agent gets identity + architecture + all prior decisions (via the cumulative log) for free from background context, plus the specific stage file on demand from GitHub. It never re-processes the other 8–9 stage files. Tokens stay minimal.

---

## 5. INTERMITTENT STRUCTURAL AUDIT (every 2–3 completed stages)

Cohesion drift is the biggest long-term risk. Run a periodic audit:

- After Stages 02 and 03 complete → first audit.
- After Stages 05 and 06 complete → second audit.
- After Stages 08 and 09 complete → third audit.
- (Adjust cadence as needed — never skip the audit before Stage 10 / Legacy.)

**How:** Spin up a SuperNinja agent. Point it at the GitHub repo. Command:

> *"Scan all completed stage files against 00_DIGITAL_TWIN_CORE.md and 00_GLOBAL_INDEX.md. Identify: (1) any logical contradictions between stages, (2) any drift from the global rules in §4 of the Global Index, (3) any place where the enterprise charter conflicts with the founder's personal operating style or energy constraint, (4) any orphaned dependencies (a stage assuming something a prior stage never actually established). Output a dated audit report; log it into the affected stage files' §7 (Audit Log)."*

Resolve every contradiction before proceeding to the next stage. The audit is a checkpoint, not optional.

---

## 6. FOUNDER DRIFT CHECK (every chat, lightweight)

Use **Structural_Checklist.pdf** alongside every stage. Tick each element as it appears in the delivered output. If a chat:
- skips an agreed element,
- changes the agreed structure mid-stream, or
- leaves items out of the final output,

→ that is a **change request**, not a silent edit. Route it through Stage 01's governance/change process. Do not accept structural changes mid-chat without recording the rationale (per the Decision Audit rule).

---

## 7. GITHUB — WHERE / WHAT / WHEN

| What | Where | When |
|---|---|---|
| Repo | Private repo `intellectual-enterprise-guidelines` | Create once, before Stage 01 |
| Stage files 01–10 | Root of repo (or `/stages/`) | Push each when its stage begins (skeletal) and again when complete (full) |
| HANDOVER_PROTOCOL.md | Root of repo | Push once; update only if the protocol itself changes |
| Completed Book .md + .pdf | `/books/` in repo | Push at each stage's close-out |
| Audit reports | `/audits/` in repo | Push after each intermittent audit |
| 00_GLOBAL_INDEX.md & 00_DIGITAL_TWIN_CORE.md | **Do NOT** put in GitHub — they live in Ninja project files (and global memory). GitHub is for the on-demand content, not the always-on anchors. | — |

**GitHub token benefit:** Stage files can be large (a completed Book may be 20–80 pages). Keeping them in GitHub means the model fetches *only the one being worked on* via RAG/agent, instead of loading all 10 into context every message.

---

*End of Handover Protocol.*
