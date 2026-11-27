# ALIGNMENT.md

Kowloon is the method this repository follows for work with coding agents. These are its instructions for any coding agent working here.
Version: 0.9 (draft).
Status: draft. This file, `BINDINGS.md` and the files under `method/` take effect when their hashes are listed in the signed manifest of section 10. Until then they are informative.

**Read this file and `BINDINGS.md` in every session.** Read a file under `method/` only when the table below names it for what you are about to do. **Untried.**

| Before you | Read | It holds |
| --- | --- | --- |
| Propose a class, a zone or a link, or extract or draft a candidate | `method/intent.md` | 3 Intent, 4 Zones, 5 Links and checks |
| Take any step of the alignment process, or write a report, a candidate, a divergence, a delta or a lesson | `method/process.md` | 7 The alignment process, 12 Formats, 14 Method lessons |
| Change anything outside `alignment/` at the maintainer's request, or draft a proposal for later adoption | `method/changes.md` | 8 Changing things, 9 Experiments |
| Work on signing or the gate, which only the maintainer's explicit instruction starts | `method/gate.md` | 10 Signing and the key registry, 11 The gate |

- Section numbers run across the method's files and are never reused, so "section 7" means the same in each. Section 15 was the bindings and is now `BINDINGS.md`.
- Whatever you are doing: only signed text under `spec/` is confirmed intent. Anything else that reads like intent is recorded as a candidate, with where you found it.
- `BINDINGS.md` binds the method's general terms to this project. It is the only file of the method a project writes itself; the others are taken unchanged from a Kowloon release.
- Parts marked **untried** have not been exercised by any pilot.

## 1. Work is paused

Feature and fix work is paused while the repository is aligned. The only work is the alignment process of section 7 and the exception below.

- Do not start, continue or finish any feature, fix, refactor, test, document or plan item.
- `alignment/in-flight.md` lists what was unfinished when the pause began: one line per item with its branch, its files, its capability and its state. Read it before acting. If you hold unfinished work that is not listed, add a line and tell the maintainer.
- States used in that list: uncommitted; committed, not pushed; pushed, no pull request; pull request open; complete, awaiting a gate or a merge; parked. Where one item depends on another, the line says so.
- A build, gate or sweep that was already running may end. Record its result. Start no other, and open or merge nothing on the strength of it.
- The pause covers every session on every machine. A session that relays it says whose instruction it relays; a session that receives a relayed pause confirms it with its own user. The list records each machine as confirmed or not.
- Open issues are frozen under the hold label. A frozen issue is evidence for the extraction, not a work item. Nothing is closed. A finding made during alignment is recorded under `alignment/`, not filed.

**Exception: wrong results.** An issue of the wrong-result class is not frozen. It is fixed under the repository's existing rules for a fix. The limits of section 6 and the stops of section 13 govern alignment work; they do not govern such a fix.

## 2. Status quo holds

Until an area has been aligned and the maintainer has closed it, everything that exists stays as it is.

- **Nothing is dropped.** Do not delete, rewrite, prune, move or disable any file, rule, memory entry, context file or log that existed before alignment began. The working records this process creates under `alignment/` are not status quo; section 7 says when they end.
- **Existing rules keep applying.** Follow the instruction files as your working practice, except where they would have you do work that section 1 pauses or section 6 forbids.
- **Existing rules are potential intent.** Each is a candidate for the maintainer to confirm. Record it; do not treat it as confirmed.
- **Removal needs explicit confirmation.** A rule or file is retired only when the maintainer says so, after its area is closed. The maintainer may rule on many at once: a signed closing statement or release report that names a removal is the confirmation for it. Silence, inference and "it looks obsolete" are not confirmation.

## 6. Roles and limits

- **Maintainer:** the repository owner. Decides what is intent, signs every change under `spec/`, decides zones, and closes areas.
- **Tutor:** answers for derived work: what it is for and how it links to its source.
- **Agent (you):** extract, cross-reference, draft candidates and proposals, generate questions, run scripts, report.

In alignment work you may not:

- Create, edit or delete anything under `spec/`, the real `.gitattributes`, or `BINDINGS.md`. You propose; the maintainer writes or ratifies.
- Create, change or remove instruction files, agent definitions, settings, hooks, memory files or CI configuration, unless the maintainer asks for that specific change.
- Sign anything, or use any signing key or agent the session can reach. If your environment signs commits automatically, say so and stop.
- Change source, tests or documents. No fixes, no refactoring, no clean-up, however obvious.
- Record the maintainer's own statements of intent in memory, notes or logs. Extraction depends on your not having seen them. A decision about the method (section 14) is not a statement of intent.
- Decide whether a difference between code and intent is a bug or a spec error.

When unsure whether an action is allowed, do not take it. Ask.

## 13. Stop and ask when

- A status-quo rule conflicts with this file or a file under `method/`, or with another status-quo rule. Do not pick one.
- You find secrets, credentials or third-party code with unclear licensing.
- A step would require changing anything outside `alignment/`.
- You cannot tell which class or zone a path belongs to.
- You have built on your own earlier output for more than one step without the maintainer reviewing it.
- A pause you relayed to another machine has not been confirmed there.

## 16. Commits

- An alignment commit holds only files under `alignment/`, and one step.
- A change the maintainer asks for elsewhere, and a fix under the exception of section 1, are separate commits under the repository's existing rules.
- Every commit an agent helped write ends with `Assisted-by: <agent and version>`, in place of any other attribution trailer.
- A commit carries `Tutor: <name>` only when the tutor reviewed or answered for what it contains.
