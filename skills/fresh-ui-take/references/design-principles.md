# Design principles

The quality bar for the new UI. The "Principles" section goes into every brief; the
checklist is for reviewing the result before it reaches the user.

## Principles

**Clear hierarchy, built with active white space.** The most important fact or action
is unmistakable at a glance. Secondary information is visibly secondary. If everything
is emphasised, nothing is. White space is a tool for this, not leftover room:
- Every gap is a decision. Active white space directs the eye, creates emphasis or shows
  a relationship. Passive white space (a gap that exists only because nothing filled it)
  carries no meaning; remove it or make it do a job.
- More space around an element raises its importance without making it bigger, bolder
  or more colourful. Reach for space before reaching for weight or colour.
- Micro space (line height, letter spacing, padding inside a component) is for
  readability. Macro space (margins, gaps between sections) sets hierarchy and how
  polished the result feels. Get both right; they solve different problems.
- Density follows the context. Data tables, dashboards and expert tools need
  compression; generous space there means more scrolling and slower scanning for people
  who already know where to look. On narrow screens, trade space against keeping the
  essentials visible without scrolling. Match the density of the project's neighbouring
  screens; never make a dense tool roomier than the app around it.

**Readable grouping.** Related information sits together and reads as one unit;
unrelated things are clearly separate. Space does the grouping: the gap inside a group
is visibly smaller than the gap between groups, so relationships read before any
border, divider or background is added. A person scanning should find each fact in one
place, labelled in the words they use.

**Every visual element carries information.** An icon, colour, badge or shape earns its
place by telling the person something: what type a thing is, a preference they set, a
status that changes what they do next. Nothing is added for decoration.
- Information the old UI carried visually is information, not styling. If an icon
  showed the item's type and a colour showed the person's chosen colour, both survive
  the redesign. Dropping them removes data.
- Combine carriers where it reads naturally (an icon that shows the type, tinted with
  the person's colour) rather than spreading one fact across several decorations, and
  never let colour be the only carrier of a meaning.
- No coloured accent borders or side stripes on cards, rows or panels. They are a
  generic decoration that carries little and makes every surface look the same.
- A badge has to pass one test: does the person need this to make a decision right now?
  "Overdue" passes; it changes what they do. A badge that restates something already
  visible, or that nobody acts on, fails. More badges is not more clarity.

**Actions are ranked, and the rank decides where they live.** Sort every action on a
component into one of four tiers:
- **Primary:** what the person should do next, the path to the outcome they came for.
  Exactly one per component. It gets the strongest emphasis and the largest, nearest
  target (filled button or equivalent).
- **Supporting:** another way to make the same main decision that can't fold into the
  primary (Approve as primary, Request changes as supporting). Visible, one step down in
  emphasis (outline or text button).
- **Secondary:** optional; it produces something separate from the main outcome and
  leaves that outcome unchanged (bookmark, export, duplicate, share).
- **Destructive:** deletes or irreversibly removes something.

An action is shown directly on the component if at least one is true: it is primary or
supporting; it shows state (a toggle such as bookmarked, pinned, following, where hiding
the action would hide the state too); or most people use it on most visits. Everything
else goes into an overflow (kebab) menu. Destructive actions go last in that menu, in a
separate section, styled as destructive, and confirmed only if they can't be undone. The
exception is a component whose job is removal (a list of items to clear out), where
remove is the primary action. Keep visible actions to about three per component; if the
test leaves more, the component is doing too many jobs.

Why: every visible choice slows the main decision (Hick's law); defer what most people
don't need now (progressive disclosure); but hidden actions get found and used less
(recognition over recall), so hide only what you accept fewer people will find. Keep
the primary target big and close (Fitts's law), keep state visible, and keep dangerous
actions away from common ones so nobody deletes while aiming for Continue.

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
- [ ] Is every gap doing a job (emphasis or grouping), are gaps inside groups smaller
      than gaps between them, and does the density match the surrounding app?
- [ ] Is everything the old UI showed visually (type icons, user-chosen colours, status
      markers) still shown? Is any icon, colour or badge there only as decoration?
- [ ] Any coloured accent borders or side stripes? Any badge the person wouldn't act on?
- [ ] Is there exactly one primary action? Are visible actions limited to primary,
      supporting, state toggles and frequent actions, with the rest in an overflow menu
      and destructive actions last in their own section?
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
