# Kowloon

A method for working with coding agents in a repository that already exists. It finds out what the code is for, has a human confirm it, and then keeps agents from changing that intent on their own.

**Status: draft 0.9. Not yet piloted.** Parts marked *untried* in the text have never been exercised. Expect it to change.

## What is here

| File | What it is |
| --- | --- |
| `HOWTO.md` | Start here. A guide for the person adopting the method |
| `ALIGNMENT.md` | What an agent reads in every session |
| `method/` | Four files an agent reads only when a task needs them |
| `BINDINGS.template.md` | The one file a project writes itself |
| `EXAMPLES.md` | Four worked spec items: hardware, agents, software, robotics. Informative |

## How a project uses it

1. Copy `ALIGNMENT.md` and `method/` into the repository unchanged, from a tagged release.
2. Copy `BINDINGS.template.md` to `BINDINGS.md` and fill it in.
3. Follow `HOWTO.md`.

A project never edits the copied files. A change to the method is proposed here, as a method lesson that says what happened and what it would change.

## What it asks of you

- One person who decides what the project's intent is, and signs it.
- A pause in feature work while the first area is aligned.
- That agents never write intent, and nothing is deleted until that person names it.

## What it does not do

It does not plan new features, generate code or replace your tests. It does not explain learned weights or vendor IP, and is not a safety case: there it binds only the assumptions, budgets and monitors around them. It is not a tool: today it is a set of documents an agent and a person follow. A reference gate script is planned and not written.
