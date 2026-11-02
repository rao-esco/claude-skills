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
   callers pass. It's the starting point for the new component, so the first swap is
   small, but it can change if a cleaner data flow needs it. Find every call site now.
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
- **Capabilities:** every action, each with its rules and limits.
- **Data in:** each entity the UI receives, with the fields that matter to a person.
- **Data out:** what each action sends, and what comes back: success, partial success,
  each kind of refusal.
- **Information shown:** facts the user needs to see, and which ones matter most.
- **States:** for every part that loads or saves, its idle, loading, empty, error and
  success states, and which of them exist today.
- **Constraints:** where it lives (dialog, page, both), the component library and icon
  set in use, permissions, hard limits, and anything the user put off the table.

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
