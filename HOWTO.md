# Starting with Kowloon

A short guide for a person bringing Kowloon into a repository. It explains and points; it carries no rules. Where it differs from `ALIGNMENT.md` or the files under `method/`, they are right. `README.md` has the one-paragraph version.

Status: Kowloon is at draft 0.9 and has not yet been through a pilot. Expect to change it after your first slice.

## What Kowloon is

Kowloon is a method for working with coding agents in a repository that already exists. It finds out what the code is for, has a human confirm it, and then keeps agents from changing that intent on their own.

It works backward first, from code to intent, and only then forward.

## What you need

- A git repository.
- A **maintainer**: one person who decides what the project's intent is. Usually the owner.
- A **tutor**: a person who can answer what a piece of work is for. It may be the maintainer at first.
- A coding agent.
- Later, not on day one: an SSH signing key held on a hardware token.

## The files

| File | Who reads it | When |
| --- | --- | --- |
| `HOWTO.md` | You | Once, now |
| `ALIGNMENT.md` | The agent, and you | Every session |
| `BINDINGS.md` | The agent, and you. You write it | Every session |
| `method/intent.md` | The agent, and you | When classifying files or writing intent |
| `method/process.md` | The agent, and you | At each alignment step |
| `method/changes.md` | The agent | When you ask for a change to code |
| `method/gate.md` | You | When the first area is about to close |

Read `ALIGNMENT.md` in full before starting. It is about 1,100 words. Skim the rest.

## First steps

1. **Copy the files in.** Put `ALIGNMENT.md` and `method/` at the repository root, unchanged.
2. **Write `BINDINGS.md`.** Copy `BINDINGS.template.md` to `BINDINGS.md` at the root and fill it in. It binds the method's terms to your project: who the maintainer and tutor are, where your packages and documents are, what your interfaces are, and which capability you will start with. Write "Not decided" where you do not know yet; the template says which step that will stop.
3. **Point your agent at them.** Add one line yourself to the instruction file your agent already reads (`AGENTS.md`, `CLAUDE.md` or the like): "Read `ALIGNMENT.md` and `BINDINGS.md` before anything else." The agent may not make this edit for you.
4. **Pause the work.** In every agent session, on every machine, say:

   > Stop all current work and start the alignment process in `ALIGNMENT.md`.

   The agent lists what was unfinished in `alignment/in-flight.md`. Nothing is deleted or finished.
5. **Let the agent run pre-flight and the inventory.** Both are read-only. You get a report of what instruction files, memory and documents exist, and whether your setup can sign and can start a blind session.
6. **Confirm the pilot.** It is the one you named in `BINDINGS.md`: one small capability (a command, an endpoint or a port-level function), the most mechanical you have.
7. **Write its intent yourself, privately.** A few sentences on what that capability must do and must never do. Keep it out of the repository, out of the chat, and out of anything the agent can read.
8. **Have the agent extract.** In a fresh session, it writes what the code actually does as candidates, with file and line for each.
9. **Compare.** Put your text beside the candidates. Each difference becomes a divergence. You decide, one by one, whether the code is wrong or your statement was.
10. **Stop and review the method.** Note what was missing, what was never used, and what got in the way. Strike the unused parts before going further.

Only after the pilot: the baseline, proposed classes, triage, and the next capability. Only when a first area is ready to close: signing and the gate.

## Your roadmap and unfinished branches

- **Plans stay as they are, with no force.** A plan item counts only when you restate it yourself as a spec item. For something not built yet, do that when work on it is about to start, not before.
- **Assume an agent wrote every plan** unless you know you did. If your own text agrees with a plan, that is not proof the plan was right.
- **Paused branches wait for their capability.** When you reach it, you either name the branch for removal or bring the work back as a new requested change or an experiment. The old branch is only a reference.
- **Afterwards the roadmap is short:** the signed items nothing serves yet, plus the proposed changes still open.

## Who does what

| You | The agent |
| --- | --- |
| Write and sign intent under `spec/` | Extracts candidates and drafts proposals |
| Rule on each divergence | Records divergences, leaves the ruling blank |
| Close an area and name what is removed | Reports and waits |
| Create the signing key and the gate | Runs the gate and reads its result |

## What you can ignore at first

Zones, budgets, signed assumptions, experiments, the order of traversal, the reading check, the release report and the gate. All are marked **untried**. The pilot needs none of them.

## Mistakes to avoid

- **Showing the agent your intent before it extracts.** The comparison only works if the two were written apart.
- **Letting the agent write under `spec/`.** It proposes; you write or ratify.
- **Cleaning up early.** Nothing is deleted until its area is closed and you have named the removal.
- **Treating a candidate as confirmed.** A candidate is what the code does, not what you want.
- **Building the gate first.** Write it when there is something signed to protect.
- **Adding rules before a pilot asked for them.** A new rule enters as a method lesson, after something happened that needed it.

## If you get stuck

Ask the agent to stop and report. Section 13 of `ALIGNMENT.md` lists when it must do so on its own.
