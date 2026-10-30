# Building, swapping and cleaning up

## Spawning the design agent

Use a fresh subagent (not a fork, which would inherit everything you've read, old
component included). A general-purpose agent with file and skill tools is right. Give it:

- the brief, as approved by the user
- where to write: a new file or folder next to the old component, named so the pair is
  obvious (for example the old name with a `-v2` or `-next` suffix, matching the project's
  file naming)
- that it must not edit any existing file: no old component, no shared hook, no API, no
  primitive. New files only.
- that it must follow the project's instructions file and conventions (code style,
  comment rules, path aliases, theme tokens), which it may read
- that it must load the skills listed under "Skills to use" before designing
- that it must not run the app's build or anything that could disturb a running dev
  server; type check and lint only
- what to report back: the files it created, any data the design needs that the
  interface doesn't provide, any rule in the brief it couldn't meet, and a plain
  statement that it didn't open the blocked files

The block is a request, not a technical lock. If the agent reports opening a blocked
file, or the result reproduces the old layout closely, tell the user and offer a rerun
with a fresh agent.

Don't hand it your conclusions about what's wrong with the old design. The brief already
says what the UI must achieve; your opinion of the old layout is exactly the bias this
skill exists to avoid.

## When the design needs data the UI doesn't get

The new component may need data shaped differently, or something extra. Judge every
option against the project's architecture standards (its instructions file and docs say
where queries, aggregation and business rules live) and against performance, not just
against "it works".

- **Fine inside the component (not heavy):**
  - presentation of a value: rendering a timestamp the way the person prefers (relative
    or exact), formatting a number or a date
  - live updates from what the person does in the component: a count that changes when
    they remove an item from a list, a selection total that follows their ticks
  - a sort the person picks, when the whole list is already loaded
- **Heavy recalculation (not a temporary fix):**
  - restructuring the input data to fit the new UI: regrouping, joining or nesting it,
    or re-sorting it into the default order the design wants (that order comes from the
    query)
  - transforming or mutating the input data before plugging it into the UI: deriving
    new records or fields from it, merging sources, rewriting values

  The query, endpoint or server should hand the component data in the shape it needs.
  Don't ship this work inside the component. Tell the user what shape the design needs,
  where the project's standards say the shaping belongs, and the query change you'd
  make; build it on their yes.
- **Wasteful fetching (also not a temporary fix):** fetching per item, fetching more
  than the view shows, or repeating a request the page already makes.
- **Sorting and pagination on the server:** when the list is paginated or filtered on
  the server, a sort the person picks is a query parameter and means fetching again.
  Sorting in the component would only reorder the loaded page, which is wrong, not just
  slow. Fetching the next page is normal, not heavy: it fetches only what the view
  shows. Keep the current page on screen while the next loads, reuse pages already
  fetched, and fetch only the page asked for.
- **Extra data the app already exposes.** Calling an existing query or endpoint from the
  new component is fine temporarily, as long as it doesn't duplicate a request the page
  already makes.
- **Data nothing exposes yet.** Stop and tell the user what's missing and why the design
  needs it. Don't fake it with placeholder values that ship, and don't change shared
  hooks, endpoints or the server without their go-ahead.

Keep a list of every temporary data workaround, with its cost. It goes in your report
and drives the cleanup.

## Swapping it in

- Change each call site to use the new component. Starting from the old props keeps the
  first swap small and going back cheap, so that's the default.
- The props aren't frozen. If the design or a cleaner, more efficient data flow needs
  different inputs (the component fetching its own data instead of receiving it, the
  parent passing less, a query returning a better shape), change them and update the
  call sites. List each change in your report. Don't bend the new component around the
  old props when that means extra recalculation inside it.
- Leave the old component's files untouched and still compiling, so going back is just
  pointing the call sites at it again.

## Verifying

- Type check and lint the new files and the changed call sites.
- Run the applicable review and stress-test skills on the new files (see
  `companion-skills.md`) and fix what they find.
- Walk the design-principles checklist.
- Look at it in the running app if one is available: each situation, each state you can
  reach. Say plainly which states you couldn't reach or check.

## Reporting to the user

- what the new design does differently, in a few lines
- the files added and the call sites swapped
- what you verified and what you couldn't
- every temporary data workaround, and what the clean version would be
- the question: keep, change, or go back

## After the verdict

**Approved:**
1. Offer to move each temporary data workaround to where the architecture standards put
   it: shape the data in the query or endpoint, drop duplicated fetching, remove
   client-side work the server can do once. Change the component's props and call sites
   to match where that's cleaner. Explain the efficiency gain in a line each. Do it on
   their yes.
2. Ask whether to delete the old component and anything only it used. Search for other
   users of each piece before deleting it.
3. Offer to rename the new files to the old names once the old ones are gone.

**Changes wanted:** iterate on the new component. If the change is about what the UI must
do, update the brief and treat it as a design change, not a patch.

**Rejected:** point the call sites back at the old component, then ask whether to keep
the new files for reference or delete them.

Nothing is committed, pushed or deleted without the user asking.
