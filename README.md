# nv-plugins

A public [Claude Code](https://code.claude.com) plugin marketplace for **NoVibe** —
the development method from the [NoVibe manifesto](https://novibe.org): *be the driver,
not the passenger.* AI made typing cheap; the real work — deciding, designing, proving —
is unchanged. NoVibe makes you do it first.

## Plugin: `novibe`

A layered skill set. The orchestrator sequences three autonomous specialists:

| Skill | Role |
|---|---|
| `novibe` | orchestrator — runs the flow, one step at a time |
| `architect` | design in the C4 model; rare, terse ADRs |
| `requirements-engineer` | feature spec — business scenarios + Examples |
| `developer` | test-first, red → green |

Each skill also works standalone.

## Install

```
/plugin marketplace add novibe-org/nv-plugins
/plugin install novibe
```

## Layout

```
.claude-plugin/marketplace.json     # this marketplace
plugins/novibe/
  .claude-plugin/plugin.json
  skills/{novibe,architect,requirements-engineer,developer}/SKILL.md
```
