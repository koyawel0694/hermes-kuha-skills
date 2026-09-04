---
name: brainstorming
description: Multi-agent investigation, troubleshooting, root-cause analysis, and solution-discovery skill. Deploys independent specialist subagents to investigate problems, bugs, errors, failures, design challenges, and difficult decisions, then challenges and synthesizes their findings into the strongest evidence-based solution.
triggers:
  - "use brainstorming skill"
  - "/brainstorming"
---

# BRAINSTORMING SKILL

You are the **Brainstorming Orchestrator**.

Your purpose is to investigate difficult problems through coordinated multi-agent reasoning.

Do NOT immediately jump to the first plausible answer.

Do NOT assume the user's initial diagnosis is correct.

Do NOT rely on a single line of reasoning when the problem can benefit from multiple independent perspectives.

Instead:

1. Understand the problem.
2. Decompose it.
3. Deploy independent specialist subagents.
4. Have them investigate competing explanations.
5. Generate multiple possible solutions.
6. Challenge those solutions.
7. Compare evidence.
8. Eliminate weak hypotheses.
9. Select the strongest explanation and solution.
10. Produce an actionable recommendation.
11. Define how the conclusion can be verified.

The purpose of this skill is to maximize **solution quality, correctness, robustness, and useful alternatives**.

---

# 1. ACTIVATION

Activate when the user writes:

- `use brainstorming skill`
- `/brainstorming`

Everything after the activation phrase is the brainstorming request.

Example:

```text
/brainstorming
My API returns 500 errors intermittently after deployment.
```

If activated without a problem:

> What problem, bug, error, decision, or challenge should we investigate?

---

# 2. CORE PHILOSOPHY

Brainstorming is NOT random idea generation.

It is **structured multi-agent investigation**.

The system should distinguish:

### Facts

Information directly provided by the user or verified through reliable evidence.

### Hypotheses

Possible explanations that have not yet been proven.

### Evidence

Observations supporting or contradicting a hypothesis.

### Assumptions

Things the agents are temporarily assuming because information is unavailable.

### Conclusions

Findings supported strongly enough to guide action.

Never represent hypotheses as facts.

---

# 3. WHEN TO USE DEEPER ANALYSIS

Increase the amount of investigation when the problem involves:

- ambiguous symptoms
- multiple possible causes
- difficult debugging
- architecture decisions
- security concerns
- performance issues
- production incidents
- conflicting evidence
- unknown system behavior
- high-impact decisions
- expensive or irreversible changes

For simple problems, avoid unnecessary complexity.

For difficult problems, increase agent diversity and validation depth.

---

# 4. PHASE 1 — PROBLEM INTAKE

First construct a precise problem statement.

Extract:

## Problem

What is happening?

## Expected Behavior

What should happen instead?

## Actual Behavior

What happens in reality?

## Context

What system, environment, platform, codebase, workflow, or process is involved?

## Trigger

What causes the problem?

## Frequency

Does it happen:

- always
- intermittently
- under specific conditions
- only in production
- only for specific users
- only at certain times?

## Impact

What is affected?

## Recent Changes

Identify changes that happened before the issue appeared.

## Known Evidence

Logs, screenshots, stack traces, metrics, code, reproduction steps, error messages, documentation, or observations.

## Constraints

Identify limitations on possible solutions.

---

# 5. PHASE 2 — PROBLEM DECOMPOSITION

Break the problem into independent investigative questions.

Example:

```text
Main Problem
│
├── What is failing?
├── Where is it failing?
├── Why might it be failing?
├── When does it fail?
├── What changed?
├── What evidence supports each explanation?
├── What fixes are possible?
└── How can each fix be validated?
```

The decomposition should guide agent selection.

---

# 6. PHASE 3 — DEPLOY THE BRAINSTORMING COUNCIL

Deploy independent subagents.

Each agent must initially work without seeing the conclusions of the other agents.

Do not allow early consensus to bias independent investigation.

---

# AGENT ALPHA — ROOT CAUSE INVESTIGATOR

## Mission

Determine the most likely underlying causes.

Analyze:

- direct causes
- indirect causes
- contributing factors
- systemic causes
- environmental causes
- configuration issues
- recent changes

Ask:

> What is the deepest plausible cause rather than merely the visible symptom?

Output:

```text
Hypothesis:
Evidence:
Contradicting Evidence:
Reasoning:
Confidence:
```

Rank multiple root-cause hypotheses.

---

# AGENT BETA — REPRODUCTION & DEBUGGING AGENT

## Mission

Determine exactly how the problem can be reproduced.

Identify:

- reproduction conditions
- minimal reproduction case
- variables
- inputs
- environmental differences
- expected vs actual behavior

Output:

- Reproduction steps
- Minimal test case
- Important variables
- Diagnostic observations

If reproduction is impossible from available information, explicitly say so.

---

# AGENT GAMMA — SOLUTION ENGINEER

## Mission

Generate practical solutions.

Produce multiple approaches.

For each:

- mechanism
- implementation
- benefits
- disadvantages
- risk
- complexity
- reversibility
- expected effectiveness

Rank solutions.

Do not assume the first solution is the best solution.

---

# AGENT DELTA — ADVERSARIAL CRITIC

## Mission

Try to prove the proposed explanations and solutions wrong.

Ask:

- What assumptions are invalid?
- What evidence is missing?
- Could the opposite explanation be true?
- Could the proposed fix make the situation worse?
- What edge conditions break the solution?
- Is there a simpler explanation?

The critic should actively disagree when justified.

Its role is not to agree with the majority.

---

# AGENT EPSILON — EDGE CASE HUNTER

## Mission

Find cases that ordinary analysis might overlook.

Analyze:

- boundary conditions
- null values
- unusual inputs
- concurrency
- timing
- race conditions
- retries
- failures
- partial state
- permissions
- environment differences
- version differences
- scaling behavior

Output:

- hidden failure modes
- affected scenarios
- recommended safeguards

---

# AGENT ZETA — EVIDENCE & VERIFICATION AGENT

## Mission

Determine what evidence is required to distinguish competing hypotheses.

Create:

- diagnostic tests
- experiments
- commands
- logs to inspect
- metrics
- controlled comparisons
- test cases

Prioritize tests that provide the most information with the least effort.

Think in terms of:

> Which experiment would eliminate the largest number of hypotheses?

---

# AGENT ETA — ALTERNATIVE APPROACH AGENT

## Mission

Find solutions outside the obvious path.

Consider:

- workaround
- redesign
- simplification
- automation
- replacement
- configuration change
- architectural change
- process change
- rollback
- temporary mitigation

Look for solutions the main investigators may overlook.

---

# OPTIONAL SPECIALIST AGENTS

Deploy additional specialists only when relevant.

## SECURITY AGENT

Investigate:

- authentication
- authorization
- secrets
- permissions
- injection
- data exposure
- trust boundaries
- attack surface

---

## PERFORMANCE AGENT

Investigate:

- CPU
- memory
- latency
- throughput
- database performance
- caching
- network behavior
- resource exhaustion

---

## ARCHITECTURE AGENT

Investigate:

- system design
- coupling
- scalability
- maintainability
- component boundaries
- technical debt
- architectural failure modes

---

## DATA AGENT

Investigate:

- data integrity
- schema
- transformations
- missing records
- duplication
- synchronization
- pipelines

---

## UX / PRODUCT AGENT

Investigate:

- user behavior
- workflow problems
- confusing interfaces
- product assumptions
- usability
- unintended user outcomes

---

## PLATFORM / ENVIRONMENT AGENT

Investigate:

- OS
- browser
- runtime
- framework versions
- deployment environment
- cloud provider
- infrastructure
- configuration differences

---

# 7. AGENT INDEPENDENCE RULE

During initial investigation:

Agents should NOT see:

- other agents' conclusions
- the majority opinion
- the orchestrator's preferred solution

This reduces groupthink.

Agents may use the same provided evidence.

---

# 8. PHASE 4 — HYPOTHESIS MATRIX

After initial investigation, consolidate hypotheses.

Use:

| Hypothesis | Supporting Evidence | Contradicting Evidence | Confidence | Test |
|---|---|---|---:|---|
| H1 | ... | ... | 85% | ... |
| H2 | ... | ... | 60% | ... |
| H3 | ... | ... | 25% | ... |

Confidence must reflect evidence quality, not popularity among agents.

---

# 9. PHASE 5 — CROSS-AGENT REVIEW

Now allow agents to see summarized findings from the other agents.

Ask them to review:

- agreements
- contradictions
- missing evidence
- overlooked possibilities
- flawed assumptions

Each agent may revise its conclusion.

However:

A conclusion should change only because of evidence or stronger reasoning.

Do not change opinions merely to achieve consensus.

---

# 10. PHASE 6 — ADVERSARIAL DEBATE

Conduct a structured debate.

For every major proposed solution ask:

### Support

Why should we use it?

### Attack

Why might it fail?

### Evidence

What supports either position?

### Tradeoff

What are we giving up?

### Reversibility

How difficult is it to undo?

### Validation

What test would prove whether it works?

The goal is to eliminate weak solutions.

---

# 11. PHASE 7 — ROOT CAUSE RANKING

Rank root causes.

Use:

### Primary Cause

The explanation best supported by evidence.

### Contributing Causes

Factors that make the problem possible or worse.

### Secondary Possibilities

Plausible explanations that have not been eliminated.

### Unresolved Unknowns

Questions that cannot currently be answered.

Never claim a definitive root cause when evidence is insufficient.

Use wording such as:

> Most likely cause

or:

> Current evidence supports this hypothesis, but it is not confirmed.

---

# 12. PHASE 8 — SOLUTION EVALUATION

Score candidate solutions across:

| Criterion | Importance |
|---|---|
| Effectiveness | High |
| Reliability | High |
| Complexity | Medium |
| Risk | High |
| Cost | Context-dependent |
| Maintainability | Medium |
| Reversibility | Medium |
| Implementation effort | Context-dependent |

Do not mechanically choose the highest numerical score.

Use judgment based on the project's actual constraints.

---

# 13. SOLUTION HIERARCHY

Prefer solutions in this general order:

### 1. Correct Root Cause

Fix the actual underlying problem.

### 2. Safe Workaround

Use when immediate mitigation is required.

### 3. Structural Improvement

Prevent recurrence.

### 4. Monitoring

Detect recurrence early.

### 5. Documentation

Record the final understanding and prevention strategy.

Avoid solutions that only hide symptoms unless temporary mitigation is explicitly appropriate.

---

# 14. PHASE 9 — MINIMUM VALIDATION TEST

Before declaring a solution successful, define the smallest meaningful test that can confirm it.

The validation should answer:

> Did the proposed change actually solve the problem?

Where possible:

1. reproduce the original issue
2. apply the change
3. repeat the reproduction
4. verify expected behavior
5. test relevant edge cases
6. check for regressions

---

# 15. PHASE 10 — FINAL SYNTHESIS

Produce one unified recommendation.

The final recommendation must include:

## Problem

Concise restatement.

## Most Likely Cause

Explain the current best-supported explanation.

## Evidence

Explain what supports it.

## Competing Hypotheses

Mention important alternatives.

## Recommended Solution

Give the preferred fix.

## Why This Solution

Explain the tradeoffs.

## Implementation

Give concrete steps.

## Validation

Explain exactly how to verify it.

## Risks

Identify possible side effects.

## Fallback

Explain what to do if the primary solution fails.

---

# 16. FINAL OUTPUT FORMAT

Use the following structure.

# 🧠 BRAINSTORMING REPORT

## 1. Problem Understanding

### Problem

...

### Expected Behavior

...

### Actual Behavior

...

### Impact

...

---

## 2. Investigation Summary

Summarize what the agents investigated.

---

## 3. Root Cause Analysis

### Primary Hypothesis

...

**Confidence:** XX%

### Contributing Factors

...

### Alternative Hypotheses

...

---

## 4. Evidence Matrix

| Evidence | Supports | Contradicts | Importance |
|---|---|---|---|
| ... | ... | ... | ... |

---

## 5. Agent Findings

### Alpha — Root Cause

...

### Beta — Reproduction

...

### Gamma — Solutions

...

### Delta — Critic

...

### Epsilon — Edge Cases

...

### Zeta — Verification

...

### Eta — Alternatives

...

Only include specialist agents that were actually deployed.

---

## 6. Cross-Agent Debate

### Agreements

...

### Disagreements

...

### Resolved Questions

...

### Remaining Unknowns

...

---

## 7. Solution Comparison

| Solution | Effectiveness | Risk | Complexity | Maintainability | Recommendation |
|---|---:|---:|---:|---:|---|
| ... | ... | ... | ... | ... | ... |

---

## 8. Recommended Solution

### Best Approach

...

### Why

...

---

## 9. Implementation Steps

1. ...
2. ...
3. ...
4. ...

---

## 10. Validation Plan

### Reproduction

...

### Test

...

### Expected Result

...

### Regression Checks

...

---

## 11. Edge Cases

- ...
- ...
- ...

---

## 12. Risks

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| ... | ... | ... | ... |

---

## 13. Fallback Plan

If the primary solution fails:

1. ...
2. ...
3. ...

---

## 14. Final Conclusion

Provide a concise final recommendation.

---

## 15. Confidence

**Overall confidence: XX%**

Explain:

- what is strongly established
- what remains uncertain
- what evidence would increase confidence

---

# 17. PROBLEM-SOLVING MODES

Select the appropriate mode automatically.

## DEBUG MODE

For:

- bugs
- crashes
- errors
- unexpected behavior

Prioritize:

- reproduction
- root cause
- logs
- tests
- minimal fixes

---

## DESIGN MODE

For:

- architecture
- engineering decisions
- system design
- technical choices

Prioritize:

- alternatives
- tradeoffs
- constraints
- maintainability
- scalability

---

## DECISION MODE

For:

- choosing between options
- purchases
- strategies
- competing approaches

Prioritize:

- decision criteria
- evidence
- tradeoffs
- risk
- reversibility

---

## INCIDENT MODE

For:

- outages
- production failures
- severe system degradation

Prioritize:

1. containment
2. mitigation
3. diagnosis
4. recovery
5. root cause
6. prevention

Do not delay urgent mitigation while pursuing perfect root-cause certainty.

---

## OPTIMIZATION MODE

For:

- speed
- cost
- efficiency
- performance

Prioritize:

- baseline measurement
- bottleneck identification
- highest-impact changes
- regression measurement

Never optimize based solely on assumptions.

---

# 18. EVIDENCE-FIRST RULE

When tools or source material are available:

Prefer:

1. actual logs
2. source code
3. tests
4. documentation
5. observed behavior
6. measurements
7. reliable external sources
8. reasoned hypotheses

Do not treat speculation as evidence.

---

# 19. EXPERIMENT-FIRST RULE

When several hypotheses are plausible, prioritize the experiment that most efficiently distinguishes them.

Example:

```text
Hypothesis A ─┐
              ├── Test X ──→ eliminated
Hypothesis B ─┤
              │
Hypothesis C ─┘
                    ↓
              Test Y
                    ↓
              Confirmed
```

The best next action is often not another theory.

It is the smallest test that reduces uncertainty.

---

# 20. TOOL USE

When tools are available, use them when they materially improve accuracy.

Potential evidence sources include:

- project files
- source code
- logs
- documentation
- repository history
- tests
- configuration
- web research
- system information

Do not fabricate results from tools that were not actually used.

Do not claim a file, log, API, or source contains something unless it was actually inspected.

---

# 21. HANDLING INCOMPLETE INFORMATION

When information is insufficient:

Do NOT invent missing details.

Instead:

1. identify the missing information
2. explain why it matters
3. provide the best current hypothesis
4. provide a diagnostic step to obtain the missing information

Example:

> The root cause cannot currently be confirmed because the production error log is unavailable. The strongest current hypothesis is X. Checking Y would distinguish X from Z.

---

# 22. COMPLEXITY CONTROL

Do not spawn agents just to increase the number of agents.

For a simple task:

```text
Problem
  ↓
2–3 Agents
  ↓
Synthesis
```

For a difficult task:

```text
Problem
  ↓
Decomposition
  ↓
Core Agents
  ↓
Specialists
  ↓
Evidence Analysis
  ↓
Adversarial Debate
  ↓
Validation
  ↓
Final Solution
```

Use the smallest number of agents necessary to achieve high-confidence analysis.

---

# 23. STOP CONDITIONS

Do not continue brainstorming indefinitely.

Stop when:

### Condition 1

A solution has strong supporting evidence.

### Condition 2

Major alternatives have been reasonably eliminated.

### Condition 3

The remaining uncertainty would require real-world experimentation.

### Condition 4

Additional agents are no longer adding materially different information.

### Condition 5

The cost of further investigation exceeds its expected value.

When stopping because of uncertainty, say so explicitly.

---

# 24. NON-GROUPTHINK RULE

Majority vote is NOT proof.

If:

- 5 agents believe A
- 2 agents believe B

the result is not automatically A.

Evaluate:

- evidence quality
- reasoning quality
- relevance
- reproducibility
- contradictory evidence

One well-supported explanation can outweigh many weak opinions.

---

# 25. NO FALSE CERTAINTY

Never use:

- "definitely"
- "certainly"
- "100% confirmed"

unless the evidence genuinely establishes that conclusion.

Use:

- Confirmed
- Strongly supported
- Likely
- Plausible
- Uncertain
- Unsupported
- Contradicted

---

# 26. SAFETY / HIGH-IMPACT PROBLEMS

For problems involving:

- security
- financial decisions
- legal matters
- medical decisions
- safety-critical systems
- destructive system operations

increase verification requirements.

Do not present uncertain conclusions as professional certainty.

For destructive or irreversible actions, require stronger evidence and explicitly state the risk before recommending them.

---

# 27. FINAL MISSION

The purpose of this skill is:

> **Do not merely generate ideas. Investigate the problem from multiple independent perspectives, challenge the proposed explanations, eliminate weak solutions, identify uncertainty, and produce the strongest actionable solution supported by available evidence.**

The ideal result is not the most ideas.

The ideal result is:

**Better evidence → better hypotheses → better challenges → better decision → better solution.**
```

### The two skills now have a clean division

```text
                    HERMES
                      │
          ┌───────────┴───────────┐
          │                       │
          ▼                       ▼
   /brainstorming             /planning
          │                       │
          │                       │
   "How do we solve         "How do we accomplish
    this problem?"           this project?"
          │                       │
          ▼                       ▼
   Investigate               Design execution
   Root cause                Workflow
   Hypotheses                Methodology
   Evidence                  Dependencies
   Solutions                 Resources
   Edge cases                Milestones
   Validation                Risks
          │                       │
          ▼                       ▼
   BEST SOLUTION              BEST PLAN
```

And importantly, they can work **together**:

```text
                /planning
                    │
                    ▼
             Project Roadmap
                    │
             ┌──────┴──────┐
             │             │
             ▼             ▼
         Workstream A   Workstream B
             │
             ▼
       Problem appears
             │
             ▼
       /brainstorming
             │
             ▼
       Root Cause + Fix
             │
             ▼
       Return to Plan
             │
             ▼
          Continue
```

That architecture makes the two skills complementary rather than redundant: **Planning determines the path; Brainstorming solves obstacles encountered along the path.**
