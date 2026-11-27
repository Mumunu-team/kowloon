# Kowloon

Kowloon proposes a methodological approach to working with coding agents in a repository that already exists. It helps you find out what the code is for, ask a human for confirmation, and then keeps agents from changing that intent on their own.

Own your codebase, declare intent, keep it under control. 

For a while at least, good grief.

## What is here

| File | What it is |
| --- | --- |
| `HOWTO.md` | Start here. Adopt the method, become a citizen of Kowloon |
| `ALIGNMENT.md` | What an agent reads in every session, what tries to keep it confirming and honoring intent |
| `method/` | Four files an agent reads on demand |
| `BINDINGS.template.md` | The one file you need to instantiate for your own project |

## When a project moves to Kowloon

1. Copy `ALIGNMENT.md` and `method/` into the repository, from a tagged release.
2. Copy `BINDINGS.template.md` to `BINDINGS.md` and fill it in.
3. Follow `HOWTO.md`.

A project should never edit the copied files.

## Citizenship requirements

- Ownership. One person who decides what the project's intent is, willing to leave their signature.
- Calm. A pause in feature work while the first area is aligned. The deep breath.
- Clear boundaries. Agents never write intent, nothing is deleted until a person names it.

## What's outside of Kowloon

The method will not help planning for new features, generating code or replacing your tests. 