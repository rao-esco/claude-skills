# The design brief

The brief is the design agent's whole world. It must be complete about behaviour and
silent about appearance.

## Rules

- **No layout.** Don't say where anything goes, what sits beside what, how many columns,
  tabs or steps there are, or what kind of control does a job (no "toggle", "dropdown",
  "tab", "chip", "sidebar", "modal stack"). Describe the job: "the user switches between
  two ways of looking at the list", not "a two-option toggle".
- **No current-UI vocabulary.** Labels the user sees can be quoted when they carry
  meaning (a status name, a domain term). Names of today's components, sections and
  visual treatments can't.
- **No code identifiers.** No file, function, hook or variable names in the body. The one
  exception is the blocked-file list, which needs exact paths.
- **Rules are features.** Limits, eligibility, permissions and validation go in, with
  what the user should be told when they hit them.
- **Say why when it isn't obvious.** "Groups don't count toward the limit because their
  members are reviewed as a list" lets the designer keep the rule's intent if they change
  the flow.
- **Placement is open.** State that the component may live inside a dialog or be embedded
  in a page, so it must work in both.

## Blocked files

List every file that belongs to this UI's current design, by exact path: the component
itself, its child components, any styles, stories, screenshots or snapshots for them.
Leave out the project's shared primitives (the component library's building blocks); the
agent needs those to build anything.

Tell the agent plainly:
- do not open, search inside, or diff these files
- do not read their version history
- do not look at the running UI or screenshots of it

Data hooks, types, API routes and the project's instructions file are allowed: they
describe data and conventions, not design.

## Template

Copy this structure. Drop a section only if it truly doesn't apply.

```markdown
# Redesign: <what the UI lets people do, in plain words>

## Context
<Product and who uses this. Where it lives: "may be shown inside a dialog or embedded in
a page, so it must work in both".>

Tech constraints: <component library> and <icon set>. Everything else (layout,
structure, interaction patterns) is open. We want a fresh perspective, not a reskin.

## The job to be done
<One short paragraph.>

## Situations
<Each context that changes behaviour, and what changes.>

## <One section per capability or group of capabilities>
<What the user can do, the rules, what they're told at each limit.>

## Information to show
<Each fact, what it means, and which matter most.>

## UI states
<Every part that loads or saves: idle, loading, empty, error, success, partial success.
What each error should tell the user.>

## Feedback after actions
<What the user learns after each action, and how much is enough.>

## Data available
<Each entity and its fields, in plain words.>

## Public interface
<What the component receives from its parent today, in plain words. Start from it so
the first swap is small; it may change if the design or a cleaner data flow needs
different inputs.>

## Design principles
<Paste the "Principles" section of design-principles.md here.>

## Skills to use
<Exact skill names from companion-skills.md, one line each on why. Or "none".>

## Off limits
Do not open, search, diff or read the history of these files, and do not look at the
running UI or screenshots of it:
- <exact path>
- <exact path>

## What we'd like back
<The new component file(s), where to put them, and the states that must be present.>
```

## Before handing it off

Read the brief as if you'd never seen the app. If you can picture today's layout from it,
remove whatever told you. If a rule appears without the message the user sees when they
hit it, add the message. Then show it to the user.
