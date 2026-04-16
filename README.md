# cole-skills

A [Claude Code](https://claude.com/claude-code) plugin marketplace by [@colefoster](https://github.com/colefoster).

## Plugins

| Plugin | Description |
|--------|-------------|
| [`security-audit`](plugins/security-audit) | Thorough, parallelized security audit of any codebase. Severity-tagged findings with CWE/OWASP IDs and concrete fixes. |

## Install

Add the marketplace once:

```
/plugin marketplace add colefoster/cole-skills
```

Then install whichever plugin you want:

```
/plugin install security-audit@cole-skills
```

Updates flow through `/plugin update`.

## Use

Each plugin's skills become available as `/<plugin>:<skill>` in any Claude Code session:

```
/security-audit:security-audit
```

…or just describe the task in natural language: *"audit this codebase for security issues"*.

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
