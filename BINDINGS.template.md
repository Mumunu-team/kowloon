# BINDINGS.md

Bindings of Kowloon <version> for <project>. Read with `ALIGNMENT.md` in every session.

Copy this file to `BINDINGS.md` and replace every line of the second column. Write "Not decided" where you do not know yet; the third column says which step will stop until you do. Delete the third column when you are done. Add a row for anything else that is specific to your project.

| Term | Here | Needed by |
| --- | --- | --- |
| Maintainer | The one person who decides intent and signs | Everything |
| Tutor | The person who answers for derived work. May be the maintainer | Extraction at detail level; the `Tutor:` trailer |
| Instruction files | Every file that instructs an agent working here: `AGENTS.md`, `CLAUDE.md`, rules and skill directories, written policies. Not agent files the product ships | The pause; the inventory |
| Packages | What a module is here: crates, packages, directories, design units | Units of intent |
| Prose | Where documents live | The inventory |
| Review log, onboarding document | Their paths and your rules for them, or "none" | Your own rules |
| Plans | Where roadmaps and plans live, including outside the repository | Plans and unfinished work |
| Interfaces | How a capability is reached: command line, HTTP, a library API, a bus, top-level ports, a topic or action, an agent entry point | Triage; extraction |
| Pilot | One small capability, the most mechanical you have | Step 1 |
| First slice | The capability aligned after the pilot | Step 5 |
| The main promise | The correctness claim the project's value rests on, in one sentence, or "none" | The project item |
| Order of capabilities | Your ranking. Default: reported wrong results; then value and risk of a silent wrong result; then shared core modules; then frequency of use | Step 5 |
| Time box per slice | A duration | Step 5 |
| Hold label | The issue label that freezes open issues | The pause |
| Wrong-result class | How an issue is marked as a wrong result, and your existing rules for fixing one | The exception to the pause |
| Where the baseline runs | The machine or job that runs the full checks | Step 2 |
| Triage tooling | Tools for coverage, fault injection and duplication, or "none" | Step 4 |
| Paths that are never lowered to supporting | A list or a file, or "none" | Zones |
| Design checker | The tool that checks design-level models, or "none" | Design properties |
| Recorded checks | Checks the gate cannot run (long, licensed, physical); where their results are kept, out of agents' reach, and who may record | The gate |
| Statistical checks | Runs, seeds, and the pinned model or simulator version, or "none" | The baseline; budgets |
| Check restrictions | Whatever narrows what a check sees here: assume, black box, bound, mock or stub, skip, waiver, retry, scenario or eval filter, simulator simplification. Recorded as a listing | The contract surface |
| External tools the gate needs | Each tool, its pinned version and its licence for unattended use | The gate |
| Other project rules that touch the method | Any existing rule that changes how a step is done here, or "none" | As it applies |
