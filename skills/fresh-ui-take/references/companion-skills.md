# Using the user's other design and UI skills

Users often install skills that encode design taste, motion rules, component-library
know-how or stress testing. A fresh take should use them: they carry the user's own
standards, and ignoring them produces a design the user then has to correct by hand.

## Find them

Look at the skills available in this session (the list the harness shows you, with
names and descriptions). Pick the ones about any of:

- visual and interaction design, polish, taste, a named designer's or platform's approach
- motion and animation: building, reviewing, performance, vocabulary
- the project's component library or design system
- mobile and touch behaviour
- accessibility
- stress-testing UI with worst-case data
- framework performance patterns for the UI layer

Judge by the description, not the name. Skip skills about documents, slides,
spreadsheets, backend, or anything that doesn't shape an interface.

## Sort them by when they may run

The design agent must not see the current UI. Some skills are safe to use during design
and some are not.

| Kind | Examples of what they do | When |
|---|---|---|
| **Principle skills** | teach how to design, animate, compose components, handle touch | During design: the design agent loads them |
| **Library skills** | how to add, compose and style the project's component library | During design: the design agent loads them |
| **Codebase-scanning skills** | audit or survey existing code, find opportunities across the repo, review a diff | Only once the new version is in place, scoped to the new files. Before that they would read the old component and leak its design |
| **Stress-test skills** | render the UI with worst-case data and report what breaks | Once the new version is in place, on the new component |

If a skill's description doesn't make clear which kind it is, read its SKILL.md before
deciding. One that "reviews" a named file or diff is safe once you point it at the new
files; one that sweeps "the codebase" is not safe during design.

## Use them

- **In the brief:** list the principle and library skills by exact name under
  "Skills to use", with one line each on why it applies to this UI. The design agent
  loads them with its skill tool before designing. Only list skills that fit: a motion
  skill for a UI with no transitions is noise.
- **Once the new version is in place:** run the relevant review and stress-test skills on the new component
  files, and fix what they find before reporting to the user. Mention which ones ran and
  what they changed.
- **Conflicts:** if two skills disagree, or a skill disagrees with the project's own
  conventions, the project's conventions win for code style; for design choices, pick
  one, say why in your report, and name the one you passed over.
- **None installed:** say so in one line and continue. The principles in
  `design-principles.md` are the floor either way.
