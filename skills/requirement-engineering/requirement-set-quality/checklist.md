# Review Checklist — Skill: `re.requirement-set-quality`

Use this checklist when executing `re.requirement-set-quality` (`v0.1.0`) to evaluate the internal quality of a requirement set.

## 0. Pre-Assessment Context & Scope Gate
- [ ] **Check Requirement Set Size:** Are at least 2 requirements provided (or a declared scope + requirement set)?
- [ ] **Check Completeness Mode:** Is the provided set a `full` specification for the bounded scope (`completeness_mode: "full"`) or a `partial` slice (`completeness_mode: "partial"`)?
  - *If `partial`:* Do NOT report missing scope items (`RSQ-01`), missing companion lifecycle requirements (`RSQ-02`), or external module prerequisites (`RSQ-05`) as confirmed defects; record them as `observation` (`not_assessable` / `insufficient_evidence`).
- [ ] **Enforce Boundary with `re.requirement-quality`:** Do NOT report single-statement lexical ambiguity (`RQ-03`), compound sentences (`RQ-05`), inline single-sentence `TBD` (`RQ-04`), or single-statement testability (`RQ-07`) under `re.requirement-set-quality`.

## 1. Scope Coverage (`RSQ-01` / `RSQ-R001`)
- [ ] If a Scope definition (In-Scope features, actors, external interfaces) is provided:
  - [ ] Does every In-Scope feature area have $\ge 1$ requirement in the set?
  - [ ] Does every declared user/system actor role have covered interactions in the set?
  - [ ] Does every declared external interface have interface requirements in the set?
  - [ ] Are explicitly Out-of-Scope items excluded from mandatory active requirements?
- [ ] If no Scope definition is provided, mark `RSQ-01` as `not_assessable`.

## 2. Set Completeness & Companion Coverage (`RSQ-02` / `RSQ-R002`, `RSQ-R003`)
- [ ] For every stateful entity or resource lock/hold introduced in the set, is there at least one valid exit/release/expiration/cancellation requirement?
- [ ] For mutating or external-facing workflows, does the set specify failure, rejection, or timeout behavior alongside the nominal path?
- [ ] Is the set free from deferred whole sections or empty capability groups marked `TBD`/`TODO`?

## 3. Internal Consistency & Contradiction Freedom (`RSQ-03` / `RSQ-R004`, `RSQ-R005`, `RSQ-R006`)
- [ ] Do any two requirements ($r_i, r_j$) mandate mutually exclusive actions, state transitions, or permissions under overlapping preconditions without an explicit precedence rule?
- [ ] Are numeric thresholds, timeouts, rate limits, field lengths, formulas, and measurement units consistent across all requirements referencing the same attribute or operation?
- [ ] Are actor names, domain entity names, and status/state enumerations used consistently across sections without unacknowledged synonym drift or homonym collision?

## 4. Uniqueness & Duplication Freedom (`RSQ-04` / `RSQ-R007`, `RSQ-R008`)
- [ ] Is the requirement set free from verbatim duplicate requirements across sections?
- [ ] Is the set free from paraphrased semantic duplicates that state the exact same obligation in different words?
- [ ] Where two requirements partially overlap on the same obligation, are they consolidated or explicitly linked rather than diverged across sections?

## 5. Inter-Requirement Dependency & Interface Coherence (`RSQ-05` / `RSQ-R009`)
- [ ] Does every internal cross-reference between requirements (e.g., `per REQ-014`) resolve to an existing requirement in the set that actually defines that rule?
- [ ] Are prerequisite states, calculated values, or events consumed by a requirement produced by at least one requirement or external interface in the set?
- [ ] Is the intra-set precondition graph free from circular dependencies ($r_i \to r_j \to r_i$)?

## 6. Set Organization, Classification & Granularity Coherence (`RSQ-06` / `RSQ-R010`)
- [ ] Are Functional Requirements, Non-Functional/Quality Requirements, Interface Requirements, and Constraints placed in their appropriate sections/categories?
- [ ] Do peer requirements in the same section operate at a coherent level of abstraction?
- [ ] Are all requirements properly grouped without unplaced structural orphans?
