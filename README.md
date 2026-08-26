# Matt-skills (fork)

This repository is a **fork** of [mattpocock/skills](https://github.com/mattpocock/skills), Matt Pocock's agent skills for real engineering. This fork exists to allow personal customization while tracking upstream changes.

## Customizations in this fork

- `implement` skill: slash-command references changed to explicit Skill tool calls, and code review must be invoked by full name `mattpocock-skills:code-review` (never the bare built-in `code-review` skill) so the two-axis Standards + Spec review always runs
- `implement-spec` skill: promoted from `in-progress/` to `engineering/` so it ships in the plugin, routed in `ask-matt`, and its closing code review likewise calls `mattpocock-skills:code-review` by full name
- `grill-with-docs` skill: added an end-of-session protocol that writes the agreed glossary terms and ADRs to disk and then stops, so the interview never silently proceeds into implementation

## License & credits

All skills and code are the work of [Matt Pocock](https://www.aihero.dev), released under the [MIT license](LICENSE). This fork is a personal modification; thanks to Matt for making these skills open source.

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
