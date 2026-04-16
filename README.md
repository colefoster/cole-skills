# claude-security-audit

A [Claude Code](https://claude.com/claude-code) plugin marketplace containing the **security-audit** skill — a thorough, parallelized security audit for any codebase that produces a severity-tagged punch list of findings.

## Install

Add this marketplace to Claude Code:

```
/plugin marketplace add colefoster/claude-security-audit
```

Then install the plugin:

```
/plugin install security-audit@security-audit
```

## Use

In any Claude Code session:

```
/security-audit:security-audit
```

…or just ask: *"audit this codebase for security issues"*.

## What it does

- **Scope discovery** — detects stack, app type, deployment surface
- **6 parallel audit agents** covering injection, auth, crypto, dependencies, deployment, DoS
- **CWE / OWASP-tagged findings** with concrete fixes
- **Severity model** based on exploitability × impact (CRITICAL → LOW)
- **Static analyzer integration** — runs `semgrep`, `bandit`, `brakeman`, `gosec`, `gitleaks`, `npm audit`, etc. when available
- **Skim-optimized output** — action header first, findings grouped by severity
- **Fix loop** — offers to fix findings CRITICAL → HIGH → MEDIUM → LOW
- **Safe verification** — non-destructive probes against dev/staging only

Works on web apps, APIs, CLI tools, libraries, and mobile codebases.

See [`plugins/security-audit/skills/security-audit/README.md`](plugins/security-audit/skills/security-audit/README.md) for full coverage details and example output.

## Repo structure

```
.claude-plugin/marketplace.json     ← marketplace manifest
plugins/
  security-audit/
    .claude-plugin/plugin.json      ← plugin manifest
    skills/
      security-audit/
        SKILL.md                    ← the skill itself
        README.md
```

## License

MIT — see [LICENSE](LICENSE).
