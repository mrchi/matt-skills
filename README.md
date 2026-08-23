# Matt-skills (fork)

This repository is a **fork** of [mattpocock/skills](https://github.com/mattpocock/skills), Matt Pocock's agent skills for real engineering. This fork exists to allow personal customization while tracking upstream changes.

## Customizations in this fork

- `implement` skill: slash-command references (`/tdd`, `/code-review`) changed to explicit Skill tool calls (`tdd`, `mattpocock-skills:code-review`) so they work reliably when the skill is invoked through the plugin

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
