# Breaking down the UI

Goal: understand the UI well enough to describe everything it must do without describing
how it looks. You read the old code so the design agent doesn't have to.

## Where to look

1. **The component tree.** Start at the file the user named (or find it from the route
   or the text they quoted) and follow every child component the UI owns. Note each
   file path: these become the blocked-file list in the brief. Stop at the project's
   shared primitives (button, input, dialog shell and similar library components); those
   are building blocks, not this UI's design.
2. **The public interface.** The props or parameters the component accepts and what its
   callers pass. It's the starting point for the new component, so the call sites
   can stay as they are, but it can change if a cleaner data flow needs it. Find every call site now.
3. **The data layer.** Hooks, queries, mutations and the API endpoints or server functions
   behind them. Record what each returns (fields, not types), what each mutation sends,
   what it answers, and how errors come back. Note the project's architecture standards
   for data too: where queries, aggregation and business rules are meant to live, how
   fetching and caching are done, and what the current UI computes in the browser that
   it shouldn't.
4. **Rules in code.** Eligibility checks, limits, permission gates, validation, what
   counts as a duplicate, which statuses exist and what each means. These are features,
   even if the UI shows them only as a disabled control.
5. **Every message.** Toasts, inline errors, empty-state text, confirmations, warnings,
   button labels that change with state. Copy them out; they tell you what the UI must
   communicate.
6. **The project's docs.** Design notes, specs, README sections and the project
   instructions file that cover this feature. They explain intent the code can't, and
   rules that hold elsewhere and must keep holding.
7. **This conversation.** Pain points, earlier decisions, and corrections the user made.
   An instruction the user gave earlier outranks your reading of the code.

## What to write down

Write it as plain language: no file names, component names or variable names. That's the
form it takes in the brief.

- **Jobs:** the one or two things the user of this UI is trying to get done.
- **Situations:** distinct contexts that change behaviour (published or draft, own record
  or someone else's, permission held or not, empty or populated).
- **Capabilities:** every action, each with its rules and limits, its tier (primary,
  supporting, secondary or destructive, as defined in design-principles.md), how often
  people use it, and whether it shows state (a toggle such as bookmarked).
- **Data in:** each entity the UI receives, with the fields that matter to a person.
- **Data out:** what each action sends, and what comes back: success, partial success,
  each kind of refusal.
- **Information shown:** facts the user needs to see, and which ones matter most.
- **Information carried visually:** every icon, colour, badge or symbol in the current UI
  that stands for a fact (an icon for the item's type, a colour the user picked, a marker
  for a status). Write down the fact, not the treatment: "each item shows its type and
  the colour the user chose for it". The design agent can't see the old UI, so a fact
  left off this list is lost. Note visual elements that carry no fact too; those are
  candidates to drop. Treatment words (icon, badge, pill, tint, filled) describe what
  you look for in the code and never appear in what you write down. A colour can be
  named only when the colour is itself the data, such as one the user chose. See the
  example below.
- **States:** for every part that loads or saves, its idle, loading, empty, error and
  success states, and which of them exist today.
- **Constraints:** where it lives (dialog, page, both), the component library and icon
  set in use, permissions, hard limits, and anything the user put off the table.

### Example: information carried visually

This example shows one way to apply the rule above, not a template to copy. The UI you
break down will carry different facts; find those, and phrase them in whatever way
reads best. Only the rule is required: write the fact, never the treatment.

Found in the code of a learning-item card: a book icon chosen by the item's type, tinted
with a colour stored on the item; an orange "Overdue" or blue "In Progress" pill; a
bookmark icon, filled or outlined; an alarm-clock icon beside the due date.

Written down:

> - Each item has a type (course, learning path, assessment). People tell types apart
>   at a glance, before reading the title.
> - Each item has a colour the person chose to tell their own items apart. It must stay
>   visible on every item.
> - Each item has a status: not started, in progress, completed or overdue. Overdue
>   matters most because it means the person should act first; the others are context.
> - Whether the person has bookmarked the item. They can change it from the item, and
>   the current state is visible without opening anything.
>
> Carries no fact (raise with the user, keep out of the brief): the alarm-clock icon
> repeats what the due date already says. Candidate to drop.

## Be critical

You are not a transcriber. Before the brief, check the request against what you found:

- **Requested workflow changes:** map the current flow step by step, then look for steps
  that can merge, steps that exist only because of an old limitation, and two routes to
  the same outcome. Propose the consolidated flow.
- **Requested features:** check whether something already does this, whether it breaks
  an existing rule, and whether it fixes the pain point or only its symptom. If a simpler
  change solves the real problem, say so.
- **Pain points:** tie each one to a cause. "Feels cluttered" might be repeated
  information, competing emphasis, or two jobs on one surface; the brief should name the
  cause, not the feeling.
- **Gaps you find:** missing states, unexplained errors, rules the UI never surfaces. List
  them for the user; they usually belong in the brief.

When your view and the user's differ, give your recommendation and the reason, and let
them decide. Don't silently drop or rewrite what they asked for.
