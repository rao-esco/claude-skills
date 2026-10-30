# Design principles

The quality bar for the new UI. The "Principles" section goes into every brief; the
checklist is for reviewing the result before it reaches the user.

## Principles

**Clear hierarchy.** The most important fact or action is unmistakable at a glance.
Secondary information is visibly secondary. If everything is emphasised, nothing is.

**Readable grouping.** Related information sits together and reads as one unit;
unrelated things are clearly separate. A person scanning should find each fact in one
place, labelled in the words they use.

**No repeated information.** Each fact appears once. A count, a name or a status shown in
two places is one place to look and one place to get out of sync. Repetition is allowed
only when the second copy does a different job (a total that confirms an action, say).

**Warnings and errors explain themselves.** Say what happened, why if it's useful, and
what the person can do next. "3 people skipped: their attempts are still in progress" beats
"Some users could not be added". Warnings (something to know) look and read differently
from errors (something failed).

**Every state is designed.** Each part that loads or saves has an idle state (what to do
first), a loading state (that keeps the layout steady and reads as the content's shape,
not a generic spinner wall), and an error state (what failed and how to recover). Add
empty, success and partial-success states wherever they can occur.

**Feedback in proportion to the change.** Saving data is routine, whether it happens
on its own (autosave) or because the person pressed Save, Submit, Assign or similar.
Confirm it quietly where it happened: the button or the changed item shows "Saving…",
then "Saved" (or the result in a few words), then settles back. No confirmation dialog
before an ordinary save, no full-screen or modal success message after it, no banner
for something the person can already see happened. Reserve a confirmation step for
actions that can't be undone or that destroy data, and keep even that to one short
question. Never silence for a destructive action, and never ceremony for a routine one.

**Changes are stated, not hidden.** When data changes, the person can see what changed
and whether it worked. Unsaved, saving, saved and failed are distinguishable.

**Works where it lives.** Usable inside a dialog and embedded in a page, at desktop and
narrow widths. Keyboard reachable, readable contrast, labelled controls, focus that
follows the action.

**Efficient by the project's standards.** Data work happens where the project's
architecture puts it. The component receives data in the shape it needs; it doesn't
restructure its input to fit the UI, or transform and mutate it before rendering. That
shaping belongs in the query, endpoint or server, so if the design needs a different
shape, say so instead of rebuilding it in the component. What the component does on its
own is presentation (a timestamp shown relative or exact as the person prefers, a
formatted number) and live updates from the person's own actions (a count that drops
when they remove an item, a sort they pick on a list that's fully loaded). On a list
paginated or filtered on the server, a chosen sort goes to the query; fetching the next
page is normal, keeps the current page visible while it loads, and reuses pages already
fetched. No per-item fetching, over-fetching or repeated requests.
Props can change to get a cleaner data flow.

**Built from the kit.** Use the project's component library and icon set as they are,
and the project's theme tokens rather than hard-coded colours, so the result looks like
it belongs and survives theme changes.

## Review checklist

Run this on the built component before reporting to the user:

- [ ] Can you tell the primary action and the most important fact within two seconds?
- [ ] Is any fact, count or label shown twice for the same purpose?
- [ ] Does every loading, empty and error state exist, and does each error say what to do?
- [ ] Do Save, Submit and similar buttons confirm inline ("Saving…" → "Saved"), with no
      dialog before or after unless the action can't be undone?
- [ ] Does it still work in a narrow container and outside a dialog?
- [ ] Can you reach and use every control with the keyboard alone?
- [ ] Does the component restructure, transform or mutate its input data instead of
      receiving it in the right shape? (Presentation formatting and live updates from
      the person's actions are fine.)
- [ ] Any per-item fetching, over-fetching or repeated requests?
- [ ] On a paginated or server-filtered list, does a chosen sort go to the query (not
      reorder only the loaded page), and does paging keep the current page visible and
      reuse fetched pages?
- [ ] Any hard-coded colours, sizes that fight the theme, or primitives edited in place?
