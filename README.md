# Matt-skills (fork)

This repository is a **fork** of [mattpocock/skills](https://github.com/mattpocock/skills), Matt Pocock's agent skills for real engineering. It exists to carry a small set of personal customizations while staying rebased on upstream. The skill catalog lives in [upstream's README](https://github.com/mattpocock/skills#readme).

## Installation

```bash
claude plugin marketplace add mrchi/matt-skills
claude plugin install mattpocock-skills@mrchi
```

Or, from inside a session:

```
/plugin marketplace add mrchi/matt-skills
/plugin install mattpocock-skills@mrchi
```

## Customizations in this fork

- `implement` and `implement-spec` close out with `mattpocock-skills:code-review`, named in full. The bare `code-review` resolves to Claude Code's own built-in review, so an unqualified name silently swaps the two-axis Standards + Spec review for a different tool.
- `grill-with-docs` stops at the documentation hand-off: it writes the glossary and the ADRs it produced and never slides into implementation on its own.

## License & credits

All skills and code are the work of [Matt Pocock](https://www.aihero.dev), released under the [MIT license](LICENSE). This fork is a personal modification; thanks to Matt for making these skills open source.
