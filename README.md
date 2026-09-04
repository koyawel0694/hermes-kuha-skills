# hermes-kuha-skills

Multi-agent project orchestration skills for Hermes Agent: plan it, break it, fix it, ship it.

By koyawel0694, built with Hermes Agent.

## Skills

| Skill | Trigger | What it does |
|---|---|---|
| kuha | `/kuha` | Master orchestrator. Takes a goal to verified completion: plans, executes, detects blockers, calls in brainstorming, replans, validates. |
| planning | `/planning` | Turns a goal into an executable plan via independent specialist agents (architect, workflow, technical, resources, dependencies, risk, validation) that debate and synthesize one roadmap. |
| brainstorming | `/brainstorming` | Investigates hard problems via independent specialist agents with competing hypotheses, challenged and synthesized into one evidence-based fix. |

Relationship: planning finds the path, brainstorming clears obstacles, kuha drives the loop.

## Install

```bash
git clone https://github.com/koyawel0694/hermes-kuha-skills.git /tmp/kuha-skills
cp -r /tmp/kuha-skills/skills/* ~/.hermes/skills/
```

Verify: `ls ~/.hermes/skills/kuha ~/.hermes/skills/planning ~/.hermes/skills/brainstorming`

## Use

```text
/kuha Build me <goal, end to end>
/planning <goal — plan only, no execution>
/brainstorming <problem, bug, error, or hard decision>
```

## Layout

```text
skills/
  kuha/SKILL.md
  planning/SKILL.md
  brainstorming/SKILL.md
```

## License

MIT — see LICENSE.
