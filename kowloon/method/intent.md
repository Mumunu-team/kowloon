# method/intent.md

Part of Kowloon, the method of `ALIGNMENT.md`, version 0.9 (draft). Read it before you propose a class, a zone or a link, or extract or draft a candidate. Section numbers run across all the files of the method.

## 3. Intent

The aim is that every artifact can be traced to an intent a human owns, a named person can explain it, and anything that fails those two tests is eventually removed, by the maintainer's decision. Until alignment reaches a path, that path has no confirmed intent.

### Classes

Only text in the normative class is confirmed intent.

| Class | Contents | How you treat it |
| --- | --- | --- |
| `normative` | Files under `spec/`, once signed by the maintainer | The only source of confirmed requirements |
| `imported` | External references: standards, datasheets, interface definitions, vendor IP, pretrained weights, hosted models | Authoritative only through a signed spec item that interprets them |
| `derived` | Source, tests, proof scripts, and any document that describes what the product does | Must link to a spec item. Until it does, it is unassigned |
| `status-quo` | Files that instruct agents working on this repository, and existing memory, context and log files. Agent files the product ships are derived | Followed as working practice under section 2. Each rule in them is potential intent |
| `informative` | Comments, commit messages, plans, issues, agent notes, prose that only explains or records, the files under `alignment/`, `ALIGNMENT.md` and `method/` while unsigned | Explanation and evidence only. Needs no intent |

- A comment that says "must", "always" or "never" is evidence, not a confirmed requirement.
- A plan item is not a mandate. Implement nothing from a plan.
- A status-quo rule tells you how to work today. It does not tell you what the project's intent is.
- A source that lives outside the repository cannot carry a path attribute. The inventory lists it with where it lives, and that listing gives it its class.

### Units of intent

Intent is written at three levels: the project; each interface capability, as one item covering every interface that exposes it; and each package or module. Items for a file, a type or a function are written only in core zones (section 4), and only to anchor a check that the module item cannot. A detail item with no `check` line is reported.

### Spec items

Written and signed by the maintainer, never by an agent.

```
id: SPEC-<area>-<nnn>
version: <n>
level: project | capability | module | detail
parent: <the spec item one level up, or none at project level>
statement: <one sentence: what must be true>
kind: purpose | refusal | behaviour | constraint | budget | assumption | hypothesis
checked-by: <check | listing | measurement | witness | review>, …
under: <assumption ids this behaviour depends on>      (only when there are any)
review-by: <YYYY-MM-DD>                                 (hypothesis only, and required there)
explained-by: <person>                                  (required in core)
```

The kind says what sort of statement the item makes. How it is verified is `checked-by`.

| Kind | Says | Usually checked by |
| --- | --- | --- |
| `purpose` | What the project, or a capability, is for: who needs it and what they lose without it. Orders work and informs rulings; never gates | Review |
| `refusal` | A non-goal: what the project will not be. Anything that can be checked is a behaviour or a constraint instead | Review |
| `behaviour` | What a capability does or promises, including what it never does | A check |
| `constraint` | A rule that can be decided from the artifacts without running the system: allowed dependencies, tool permissions, licences, clock-domain and reset rules, data that may leave the host | A listing or a linter |
| `budget` | A numeric threshold: run time, memory, size, a pass rate. A property that is not a number, such as determinism, is a behaviour. **Untried** | A measurement |
| `assumption` | What the environment must provide for a behaviour to hold. **Untried** | A witness run |
| `hypothesis` | A question an experiment is meant to answer. **Untried** | Nothing, until promoted |

- **Universal claims.** In core, a behaviour whose statement says "always", "never" or "for all" is not covered by example tests alone. It needs a property, a differential run or an exhaustive check. A claim that something eventually happens carries a bound when tested; when model-checked, its fairness assumption is in `under:`. The maintainer judges both when signing; the gate cannot.
- **The main promise is written down.** A project whose value rests on a correctness claim states that claim as a project-level behaviour. `BINDINGS.md` names it.
- **Assumptions are tied to what depends on them.** Every assumption is named in the `under:` of at least one behaviour. One that is not is reported.

**Retirement.** When a capability is removed, its items are deleted, not kept as history. An id is never reused. A `refusal` may remain to say the capability is gone on purpose.

**When the version is bumped.** Bump when a reader who had verified the old text would have to verify again: the statement asks for something different, more or less; a term in it now means something else; `level`, `parent`, `kind` or `checked-by` changes. Do not bump for spelling, formatting, a clearer wording of the same requirement, or a change of `explained-by`. When in doubt, bump.

## 4. Zones

**Untried.** The zone of a path decides how much binding it gets. Two zones are assigned. The rest are derived or generated, and need no signature.

| Zone | How it is set | Binding |
| --- | --- | --- |
| `core` | The default for every path. Checks, their harness and the gate are core, because a fault in them can hide a fault elsewhere | Detail items where needed, checks with negative controls, the tutor answers for it |
| `supporting` | Earned. A path is supporting only when a named check has a negative control that is a fault injected in that path, which shows a fault there is loud | The module item and its link. Ordinary tests |
| experimental | Derived: the path's intent is a `hypothesis` item | The isolation of section 9 |
| unexplained | A generated finding: reachable code no one can explain, behaviour no item asks for, or interfaces or documents that disagree | Frozen: no change without the maintainer, and no new code may depend on it (checked by review). A dated question to the maintainer, paths that can change a result first; reported at every gate run while overdue |
| unreachable | A generated finding: reached by no capability, duplicated or redundant | Removal in a batch the maintainer signs (section 7), after ruling out an experiment |

- Lowering a path to supporting needs the fault-injection check and the maintainer's signature on `.gitattributes`. Returning it to core needs nothing.
- If that check is removed or weakened, the path is core again.
- A module that is core for any capability is core.
- A path that `BINDINGS.md` lists as never lowered stays core.
- Where code is core and also dominates run time, a simple reference implementation is worth keeping if one exists or is cheap to write. Agreement of the optimised code with it is then a check.

## 5. Links and checks

Each fact is recorded once.

**`.gitattributes` is the record for paths.** It gives every tracked path a `class`, and every derived path a `zone` and an `intent`, by pattern where a directory is uniform. `intent` is `unassigned`, or one or more spec ids with the version the link was made against, separated by commas with no spaces:

```
*                  class=derived       intent=unassigned
spec/**            class=normative
alignment/**       class=informative
AGENTS.md          class=status-quo
src/parser/**      class=derived       zone=supporting   intent=SPEC-PAR-001@1
src/report/**      class=derived       intent=SPEC-REP-001@2,SPEC-REP-004@1
notes/**           class=informative
```

Later lines override earlier ones, so every path the first line catches by mistake needs a line of its own: `.gitattributes` itself and the method's files are `informative` while the method is unsigned. Only `.gitattributes` gives a path intent. `zone` is `core` or `supporting`; a path with no zone is core.

**The trace map is the record for what is finer than a path.** One line per link, kept beside the spec, so that no source file is edited to record a link:

```
<spec id>@<version>   symbol   <path>::<function, type, or section heading>
<spec id>@<version>   check    <runner>:<the check's name as that runner lists it>[=<expected outcome>]
```

For example, `SPEC-FIFO-003@1   check   formal:fifo_top.a_no_overflow=proved`. An outcome other than the expected one, such as a timeout or a pass bounded to some depth, is not a pass.

A `symbol` line may only narrow. Its item must be the one its path already links to, or a descendant of that item through `parent:`. A map line never gives intent to a path that has none, which is why the map needs no signature.

**A link is stale** when the spec item's version is higher than the version in the link.

**One mechanism for everything that verifies.** A link to a check needs one thing: a stable name that a tool can list.

| Kind of check | Its name | The tool that lists and runs it |
| --- | --- | --- |
| A test | The test's full name | The project's test runner |
| A named assertion in a hardware design | The assertion's label | The verifier, which reports a verdict per label |
| A property of a design model | The formula's name in the model | The design checker |
| A budget (**untried**) | The measurement's name | The script that measures and compares |
| A runtime monitor or enforcement point (**untried**) | The monitor's name | The harness that injects a violation and observes the monitor act |

An assertion written inline in ordinary code has no stable name. It is covered by the `symbol` line of its function and by that function's tests. If it matters enough to link, it is given a test, and the test is the link.

- **Every check can fail.** A check that carries intent keeps a negative control beside it: a planted violation, a failing parent commit, a mutation, or a broken variant of a model. The control runs under the check's own assumptions, bounds and harness. A check with none is reported as unproven, not as passing.
- **Which tests need a line.** A test that protects a signed statement has a `check` line. A test with no line belongs to its path's `intent` and may change with the code it tests.
- **Characterisation checks. Untried.** A `check` line whose id is a candidate pins current behaviour and not intent. Write these before refactoring thinly covered code. When the candidate is ruled on, the line moves to the spec item or the check is removed.
- **Budgets. Untried.** Two or three per capability, measured with experiments off. Prefer deterministic counters to wall-clock time, which is recorded as a trend unless time is the promise (a deadline, timing closure). Compare against the alignment baseline, not the previous commit; the baseline is a starting point, not approval of the size. Loosening a number is a version bump.
- **Design properties (optional).** Where a design-level statement can be modelled, the model's properties are checks like any other, with a broken variant of the model as the negative control. This checks the model; that the code behaves like the model rests on the tutor's answer, or on an extractor where one exists.
