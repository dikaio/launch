# Launch

A starter repository for building a product with an AI coding agent — **Claude Code** or **Codex** — using a docs-first workflow:

```text
IDEA → PRD → DESIGN TOOL → DESIGN.md → BUILD.md → CODE → TEST → DEPLOY
```

The agent guides you step by step, in plain English, and won't start coding until the product, design, and technical plan are defined. No technical background required.

## Quick start

```bash
git clone https://github.com/dikaio/launch.git my-project
cd my-project
rm -rf .git && git init   # start your project with a fresh history
```

Then open the folder in your coding agent:

- **Claude Code:** run `claude` inside the folder
- **Codex:** run `codex` inside the folder

And paste:

> Start the project playbook. I want to build: [describe your idea normally]. Do not code yet. Guide me through Step 1 and help me create the PRD first.

## How it works

| File | Purpose |
| --- | --- |
| `AGENTS.md` | The playbook. Codex reads it automatically. |
| `CLAUDE.md` | One line, `@AGENTS.md`, so Claude Code loads the same playbook. |

Edit `AGENTS.md` only — both agents always follow the same instructions. Start your agent from the project folder so it picks them up, and start a new session after changing the playbook.

As you work, the agent creates:

```text
docs/
  PRD.md        # what the product does
  DESIGN.md     # how it looks and feels
  BUILD.md      # how it's engineered and shipped
references/
  <tool-name>/  # exports from your design tool(s), e.g. aura/
```

## Design tools

[Aura.build](https://www.aura.build) is the suggested design tool, but any visual design tool works — v0, Figma, Google Stitch, Lovable, or a mix. Design exports are treated as visual references; the production code follows `docs/DESIGN.md` and `docs/BUILD.md`.

## More prompts

`AGENTS.md` includes copy/paste prompts for resuming a project, returning from the design tool, starting implementation, adding features, fixing designs, and preparing to ship.

Once your project is underway, replace this README with one describing your product.

## License

[MIT](LICENSE)
