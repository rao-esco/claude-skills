---
name: fresh-ui-take
description: Get a fresh, unbiased redesign of an existing UI area (a dialog, panel, page section or component). Breaks down what the UI does, writes a layout-free brief for a design agent that is blocked from reading the current component files, has it build the new version, puts it in place of the old files (git keeps the old version), and keeps any data changes temporary until the user approves the design. Use this whenever the user wants to redesign, rethink, re-imagine or get a "fresh take", "new perspective" or "different approach" on a screen or component, says a UI feels cluttered, confusing or outdated and wants it reworked, or asks for a design brief or prompt for a design agent, even if they never say "fresh take".
---

# Fresh UI take

The point of this skill is a redesign that is not anchored on the current one. Whoever
designs the new version learns what the UI must do, what data it gets and what it must
communicate, and nothing about how it looks today. You do the understanding; a design
agent that has never seen the old layout does the designing; the new version replaces the
old files at the same paths, and git keeps the old version so going back is one restore.

## Workflow

### 1. Pin down the target

The user names the UI they want rethought ("the assign course dialog", "the results
table filters"). If they don't, or the name matches several places, ask which one before
doing anything else. A redesign of the wrong thing is pure waste.

Also capture, in their words:
- what bothers them about it now (pain points), if anything
- whether they want the same job done better, or a changed workflow
- anything that is off the table (a deadline, a part that must stay, a backend that can't change)

### 2. Break the UI down

Read [references/breakdown.md](references/breakdown.md) and follow it. You end up with a
plain-language inventory: the jobs the UI does, every capability and rule, the data it
receives and sends, every message it shows, every state it can be in, and its
constraints. Sources are the code, the project's docs, and this conversation.

Be critical here. If the user asks for a new workflow, map the current one first and look
for steps to merge or drop. If a requested feature duplicates one that exists, conflicts
with a rule, or solves the pain point at the wrong level, say so and suggest the better
option before writing anything. Agree the scope with the user when it changes.

### 3. Write the design brief

Read [references/design-brief.md](references/design-brief.md) for the template and its
rules, and [references/design-principles.md](references/design-principles.md) for the
quality bar the brief must carry. The brief describes features, data, information shown,
outputs and constraints. It says nothing about layout or about the current UI's elements,
and it lists the component files the design agent must not open.

Check which of the user's other design and UI skills apply, following
[references/companion-skills.md](references/companion-skills.md). Skills that teach
principles go into the brief for the design agent to load; skills that scan existing
code wait until the new version is in place, because they would show the agent the old
design.

Show the brief to the user before handing it off. They know the domain better than any
file; a wrong assumption caught here costs one message instead of a rebuilt component.

### 4. Have the design agent build it

Read [references/build-and-swap.md](references/build-and-swap.md). First make sure the old
component's files are committed, because they're about to be replaced and git is the only
copy you'll go back to. Then spawn the design agent with the brief, the blocked-file list
and a staging folder inside the old component's folder. It writes only there and never opens or
edits the old files.

### 5. Put it in place, check it, report

As soon as the agent finishes, replace the old component's files with the staged ones at
the same paths, so the call sites keep working and the repo holds one version. Verify
(type check, lint, the running app where possible). Run the applicable review and
stress-test skills on the new files and fix what they find. The component may format
values for display and update live from the person's actions. It must not restructure,
transform or mutate its input data to fit the new design: that's heavy recalculation, so
judge where it belongs by the project's architecture standards and propose the query or
server change instead. Props can change if a cleaner data flow needs it. Shared hooks,
APIs and server code change only with the user's go-ahead. Report what changed, what was
verified, every temporary data workaround, and the commit the old version can be
restored from.

### 6. After the user's verdict

- **They like it:** offer to move the temporary data shaping to where it belongs (the
  query, hook or endpoint) so the component stays clean and the data layer stays
  efficient. There's no old component left to clean up.
- **They want changes:** iterate on the new component; update the brief first if the
  change is about what the UI must do rather than how it looks.
- **They don't like it:** restore the old files from the commit you recorded and remove
  the files only the new design added.

Apart from replacing the old component's own files, which git keeps, nothing is deleted,
no shared data code is changed, and nothing is committed without the user saying so.

## Reference files

| File | Read it when |
|---|---|
| [references/breakdown.md](references/breakdown.md) | Step 2: understanding the current UI and the user's need |
| [references/design-brief.md](references/design-brief.md) | Step 3: writing the brief for the design agent |
| [references/design-principles.md](references/design-principles.md) | Step 3 (it goes into the brief) and step 5 (to review the result) |
| [references/companion-skills.md](references/companion-skills.md) | Step 3 (which skills the design agent loads) and step 5 (which review skills run on the result) |
| [references/build-and-swap.md](references/build-and-swap.md) | Steps 4 to 6: spawning the agent, replacing the old files, data changes, going back |
