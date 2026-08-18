# cole-skills

A [Claude Code](https://claude.com/claude-code) plugin marketplace by [@colefoster](https://github.com/colefoster).

## Plugins

| Plugin | Description |
|--------|-------------|
| [`dumb-down`](plugins/dumb-down) | Re-explain the previous response (or a specified topic) in plainer language — ELI30-but-tired. |
| [`google-style`](plugins/google-style) | Speak and write in Google developer documentation style for the rest of the session. |
| [`kaomoji`](plugins/kaomoji) | Express yourself with kaomoji — Japanese-style text emoticons — for the rest of the session. |
| [`step-back`](plugins/step-back) | Pause hands-on work and reassess an area from a higher level — ideal architecture vs. accrued friction. |
| [`three-designs`](plugins/three-designs) | Spawn 3 parallel sub-agents to produce 3 radically different design solutions, each using a distinct mental model. |
| [`two-claudes`](plugins/two-claudes) | Stress-test a plan by grilling it with codebase access and sending each question to an independent expert agent for fresh perspective. |
| [`wrap-up`](plugins/wrap-up) | End-of-session wrap-up: save durable knowledge to memory, then commit the session's code changes in clean, scoped commits. |

## Install

Add the marketplace once:

```
/plugin marketplace add colefoster/cole-skills
```

Then install whichever plugin you want:

```
/plugin install wrap-up@cole-skills
```

Updates flow through `/plugin update`.

## Use

Each plugin's skills become available as `/<plugin>:<skill>` in any Claude Code session:

```
/wrap-up:wrap-up
```

…or just describe the task in natural language: *"let's wrap up this session"*.

## Repo structure

```
.claude-plugin/marketplace.json     ← marketplace manifest
plugins/
  <plugin-name>/
    .claude-plugin/plugin.json      ← per-plugin manifest
    skills/
      <skill-name>/
        SKILL.md                    ← the skill itself
```

## License

MIT — see [LICENSE](LICENSE).
