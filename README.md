# toilet-entropy-reset

Toilet cleaning is a control loop.

Humans add entropy.
The machine detects deviation from a target hygiene state.
The machine runs a reset policy.
Repeat forever.

---

## The Story: From XDG to Entropy Reset

### Act 1: XDG Conventions

In 2003, the Linux desktop was a mess. Every application dumped files wherever it wanted:

```
~/
  .mozilla/
  .opera/
  .gnome/
  .kde/
  .adobe/
  .macromedia/
  ...chaos
```

Then came the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/latest/): three canonical locations:

- `~/.config` for configuration
- `~/.local/share` for data
- `~/.cache` for cache

Suddenly, tools could find things. Users could manage configs. The chaos became order.

### Act 2: The Home Directory Cleanup

In July 2026, a developer's home directory had 45+ cluttered entries. Dotfiles everywhere. Duplicate directories. Go workspace in `~/go`. Maven in `~/.m2`. Rust in `~/.rustup`. Three separate npm directories.

The fix was the same principle: **move everything to canonical locations**.

- `~/.m2` → `~/.config/m2`
- `~/.rustup` → `~/.local/share/rustup`
- `~/.docker` → `~/.config/docker`
- `~/Career`, `~/Work`, `~/Kerja.Work` → `~/Work/`

We added enforcement hooks that warn when you try to create files in the wrong place. We set up monitoring to detect violations. We scheduled periodic audits.

**The pattern emerged: define canonical state → detect drift → enforce compliance → repeat.**

### Act 3: The Leap

Then the question hit: **why stop at files?**

A home directory is just a collection of state. Files in wrong places = clutter. A physical home is the same: shoes on the floor, dishes in the sink, clothes on the chair.

**Cleaning is entropy reset.**

Humans increase entropy by living. Machines can run cron-like jobs to project the home back onto a low-entropy target manifold.

### Act 4: Why Toilets First?

Because toilets are the **perfect first wedge**:

| Property | Toilets | General Tidying |
|----------|---------|----------------|
| Surfaces | 5-6 | 50+ |
| Object classes | 10 | 200+ |
| Deviations | Measurable (stain score, wetness) | Subjective ("messy") |
| Safety | Low risk | Breakables, kids, pets |
| Utility | High (hygiene) | Variable |
| Repetition | Daily | Variable |
| Ambiguity | Low (clean = clean) | High ("tidy" varies by culture) |

A toilet reset loop is a much better first milestone than "general humanoid maid."

---

## Core Concept

A toilet is considered **pristine** when:

- Bowl interior within stain threshold
- Seat dry
- Rim clean
- Floor dry
- No visible debris
- Consumables above threshold (toilet paper, soap)
- Odor below threshold
- Bin not full

The loop:

```
1. Observe current state
2. Compare against target state
3. Generate deviation list
4. Plan minimal corrective actions
5. Execute
6. Verify
7. Log result
8. Sleep until next trigger
```

---

## Repo Structure

```
toilet-entropy-reset/
  README.md                    # This file
  LICENSE                      # MIT
  spec/
    toilet-state.yaml          # Target state schema
    home-state.schema.json     # Full JSON schema for any room
  policies/
    default.yaml               # Cron and event triggers
  agents/
    perception_agent.md        # Vision/VLA perception spec
    planner_agent.md           # Task planning spec
    executor_agent.md          # Robot dispatch spec
  reference/
    xdg_mapping.md             # XDG_HOME_KEYS, XDG_HOME_SHOES, etc.
    object_taxonomy.md         # Object classification
```

---

## Triggers

- `cron: 0 */4 * * *` (every 4 hours)
- `event: post_use`
- `event: odor_spike`
- `manual: guest_mode`

---

## Why This Exists

Most people talk vague "smart home" nonsense. This repo defines a **tight, machine-enforceable state model**.

Future robots can consume whatever spec is here. The schema is the contract.

---

## License

MIT
