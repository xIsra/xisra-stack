# xisra-stack

Reusable [Agent Skills](https://agentskills.io) by [Israel Kouperman](https://xisra.com). Each skill is a folder under `skills/` with a `SKILL.md`, so it works with any agent the [skills CLI](https://skills.sh) supports.

## Install

```bash
npx skills add xIsra/xisra-stack                        # pick skills interactively
npx skills add xIsra/xisra-stack --skill explain-flow   # one skill
npx skills add xIsra/xisra-stack --list                 # list without installing
```

## Skills

| Skill | Use it to |
| --- | --- |
| [explain-flow](skills/explain-flow/SKILL.md) | Trace how data moves through code as one `→` chain of real hops, from trigger to the field that changed. |

## License

[MIT](LICENSE)
