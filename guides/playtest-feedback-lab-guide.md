# Avalon Partner Playtest & Feedback Lab

**Free creator tool presented by Captain Amado**  
**Version 1.0 | October 21, 2026**

## What the app helps you do

Open [`tools/playtest-feedback-lab.html`](../tools/playtest-feedback-lab.html) in a browser to plan a playtest, record what people did, connect findings to their evidence, choose a change, and compare a later test. The central question is: **What happened when someone played this version of the game, and what should I test next?**

The app is a single HTML file with embedded CSS and JavaScript. Its core workflow works offline, with no account, paid API, external font, build step, or backend. Source links and any recording links you supply require their destination to be available. The app does not record participants, run your game, inspect game URLs, collect telemetry, or connect to Roblox Studio, Steam, or another Avalon tool.

The HTML contains the application. A downloaded project JSON file contains your work. Keep both.

## Start here

1. Open the HTML file in a current browser.
2. Choose **Explore the completed example** to learn the workflow, or **Start an empty project** to use your own game.
3. Complete the **Project profile**. This profile travels with your Avalon project file. Each test still keeps its own build and audience context.
4. Create a test and work through **Question**, **Context**, and **Session kit**.
5. Record sessions using a tester alias. Reuse the same tester record when the same person plays again.
6. Add specific evidence notes, then group them into findings.
7. Review a suggested follow-up or write your own action. Record your decision, proposed change, success measure, and later result.
8. Export the project JSON after meaningful work. Use the reports and CSV exports when you want to share readable material.

An open form has its own unsaved edits. Save the form before exporting. Canceling or closing an edited form asks whether to discard those changes. Loading an example, opening another project, or starting a blank workspace presents a replacement review before the active project changes.

## A practical session workflow

### 1. Ask one useful research question

Choose from six templates:

| Template | Useful question |
|---|---|
| First-time onboarding | Can a new player discover the first meaningful objective? |
| Core-loop clarity | Does the player understand how actions produce progress and what to do next? |
| Difficulty and recovery | Can the intended player complete a challenge and understand an unsuccessful attempt? |
| Multiplayer participation | Can each participant enter the activity and contribute? |
| Controls and input | Can the player perform essential actions on the target device and input? |
| New update or changed feature | Can returning players discover and use the changed feature? |

The templates are original, editable starting points. Their criteria are planning choices, not universal Roblox or industry benchmarks.

State the task and visible success criterion before running sessions. For example, “collect a parcel and begin moving toward its destination without a hint” is an observable criterion. “Understand the game” needs a more specific behavior before it can be scored consistently.

Use the metric identifier for a stable definition, such as `first-delivery-started`. Keep that identifier when the task metric remains unchanged. Changing the identifier, task, criterion, or study context causes the comparison screen to expose the difference.

### 2. Record the context

Record the exact build, dates, intended audience, device, input method, and recruitment context. Include relevant prior experience, whether people already know one another, incentives, or other selection limits in the audience and recruitment text.

Use the observer worksheet to define timing boundaries. Specify what starts an attempt, what ends it, when the task ends, and how you will handle requests for help. For multiplayer sessions, record group size and roles. Simulated clients are software instances and do not count as additional human testers.

A device simulator and a physical device provide different evidence. Label the environment you actually used. Roblox documents its own client/server, multi-client, device, controller, and network testing options in [Studio testing modes](https://create.roblox.com/docs/studio/testing-modes), reviewed October 21, 2026.

### 3. Run the task without giving away the answer

Edit the neutral instructions to fit your game. Give the player a meaningful goal without naming the specific button, route, or cue whose discoverability you are testing. Record any hint or guidance you provide. This follows the task-design principles in the [GOV.UK moderated usability testing guide](https://www.gov.uk/service-manual/user-research/using-moderated-usability-testing), reviewed October 21, 2026.

The session form separates two different judgments:

| Field | Meaning |
|---|---|
| Session status: completed | Observation reached the planned endpoint. The task may have succeeded or failed. |
| Session status: incomplete | Observation stopped before the planned endpoint, for example because of an interruption. |
| Criterion: yes | The entered success criterion was met. |
| Criterion: no | The entered success criterion was not met. |
| Criterion: unknown | The outcome was not established. |

A completed session can contain a recorded “no.” An incomplete session is excluded from the completed-outcome metric even if someone entered “no.” A blank numeric field stays unknown; it does not become zero.

Enter task attempts only when counted. Enter elapsed seconds only when measured. Optional start and end timestamps can supply a calculated duration if the elapsed-seconds field is blank. An explicit elapsed value takes precedence over timestamps.

Use the behavior questions to ask what the player did, noticed, or understood. Use the preference questions separately to ask what they enjoyed or would change. Leave unanswered questions unanswered.

### 4. Capture specific moments

Add one note for each useful moment, with an optional elapsed-second marker and creator-selected tags.

| Note type | Example |
|---|---|
| Direct observation | “Walked past the board twice and did not collect a parcel.” |
| Player quotation | “I do not know what my job is.” |
| Observer interpretation | “The board may blend into the scenery.” |
| Proposed solution | “Try a clearer parcel silhouette.” |
| Bug | “The touch control overlaps the parcel label on this handset.” |

The interpretation and solution are ideas to investigate. A quote reports what the player said; it does not independently establish the behavior they describe. The separation reflects the observation and analysis approach in [Analyse a research session](https://www.gov.uk/service-manual/user-research/analyse-a-research-session), reviewed October 21, 2026.

No personal information is required. A recording link is optional and supplied by the creator. The app only stores the link; it does not make or upload a recording.

### 5. Group findings and review evidence

You can create a finding manually and select its notes or source sessions. You can also group tagged notes into findings after reviewing the groups. Extending one existing finding keeps its ID and written summary. When several findings share the same tag in a test, edit their evidence explicitly rather than choosing a winner automatically.

Matching rules use **case-insensitive literal substring matching**. They suggest tags for review. For example, a rule containing `objective` can also match “no objective problem,” so the creator must decide whether to apply it. Rules do not interpret meaning and do not run regular expressions.

The default editable rules are:

| Literal text | Suggested tag | Note type |
|---|---|---|
| `objective` | `objective-visibility` | Direct observation |
| `control` | `controls` | Direct observation |
| `stuck` | `difficulty` | Direct observation |

Editing a rule does not rewrite existing notes. Review and apply new matches explicitly. Manual tags remain available.

A finding shows linked source IDs, affected tester counts, the denominator, device/build context, note types, and missing evidence. Severity is your judgment: low for minor friction, moderate for an interruption, high for a blocked task, and critical when a tester cannot continue safely or at all. Severity is not an automated confidence score.

### 6. Choose a change and test it again

A supported finding tag can produce an explicit suggestion. The current supported tags are `objective-visibility`, `controls`, `difficulty`, `bug`, `core-loop`, and `multiplayer`.

A candidate requires a finding that is not resolved and has linked source sessions. The suggestion explains the exact tag rule, the linked completed-tester count, excluded incomplete evidence, and limitations. Missing direct observations produce a request to collect direct evidence. A suggested change is a local planning rule, not proof of a cause. Review missing-evidence warnings before accepting it.

Accept or reject the suggestion and record why. Define the change, the visible success measure, and the later test. Record the later result even if the change did not help. You can also create a reviewed action without using a generated suggestion.

## How counts and comparisons work

### Stable identities

Every project, tester, test, session, note, finding, rule, and action receives an internal UUID. Renaming a tester alias does not change the tester ID. Two people may share an alias and still count as two testers. Repeated sessions from the same tester count once in each distinct-tester metric.

The project ID is generated once and retained across exports and imports. A matching project name is not identity. Explicitly duplicating the project creates a new project ID.

### Metric definitions

Metrics apply to the selected test. For each metric, the app chooses the **earliest eligible completed session per tester ID**, ordered by session date, then creation timestamp, then stable session ID. If the date is blank, the date part of the creation timestamp supplies the ordering date.

Each metric selects its own eligible sessions. An earlier unknown value does not prevent a later known value from supplying that metric. Different metrics may therefore use different sessions for the same tester.

| Metric | Numerator or value | Denominator or measured sample |
|---|---|---|
| Task criterion met | Distinct testers with selected outcome `yes` | Distinct completed testers with selected outcome `yes` or `no` |
| Task criterion not met | Distinct testers with selected outcome `no` | The same known-outcome denominator |
| Assistance | Distinct testers with selected assistance `prompt` or `guided` | Distinct completed testers with known assistance `none`, `prompt`, or `guided` |
| Duration | Median, mean, minimum, maximum, and individual seconds where available | Distinct completed testers with an entered duration or valid start/end interval |
| Finding coverage | Distinct completed testers in the finding's linked sessions | All distinct completed testers in that test |

A percentage is `numerator / denominator × 100`. It is unavailable when the denominator is zero. Counts are shown first.

Duration includes measured unsuccessful completed sessions as well as successful ones. A short unsuccessful attempt is not automatically a better result. Missing durations remain excluded from the duration sample, and the sample count should be considered alongside completion and assistance.

Finding coverage combines explicitly selected source sessions with sessions attached to selected notes, then deduplicates the tester IDs. This is **documentation coverage**, not a verified failure rate. No note about a problem does not prove that a player was unaffected. Session-only links count as creator-selected evidence, with missing direct-note warnings shown separately.

### Comparing later tests

The app supports descriptive comparison of completion, assistance, and duration. It checks the recorded metric identifier, task, success criterion, audience, device, input, and recruitment context. Blank or differing values block a calculated delta. These are exact text checks after trimming surrounding spaces, not semantic comparisons.

It also checks observed session contexts. Mixed builds/devices/inputs, missing completed-session context, or disagreement between planned and observed context can block the calculation. Different versions and dates remain visible and are expected in an ordinary later-build comparison. Reused testers produce a familiarity warning.

Duration comparisons additionally require nonblank matching observer worksheets. That is a documentation check, not proof that the timing boundaries were applied consistently. The comparison screen requires your confirmation of the same timing start and stop rule before revealing a duration delta. The app identifies elapsed entries and timestamp-derived intervals, both expressed in seconds.

For compatible measured samples, the delta is:

- Completion or assistance: later percentage minus earlier percentage, in **percentage points**.
- Duration: later median minus earlier median, in **seconds**.

When conditions are incompatible, the app shows separate raw results and the differences. It does not calculate an improvement delta. An ordinary before/after comparison is not a randomized experiment and does not establish causation, population effects, or future retention.

## What to inspect in the fictional example

**Moonlight Couriers** is invented teaching data.

| Test | Context | Recorded result |
|---|---|---|
| 01 / Find the first delivery | Build 0.3.0; first-time desktop players | Three of eight distinct completed testers meet the criterion. Five do not. |
| 02 / Retest the brighter delivery board | Build 0.3.1; eight fresh testers with the same stated task and context | Seven of eight meet the criterion. This is a descriptive later sample. |
| 03 / Returning players on touch | Build 0.3.1; returning phone players, changed task and recruitment | Two of three meet a different criterion. The comparison exposes the mismatches. |

Test 01 contains ten session records: nine completed records representing eight testers, plus an incomplete session for a ninth tester. Repeated notes and a repeated completed session from Aster do not inflate the five affected testers.

The objective finding contains seven direct observation notes from five testers. Its reviewed action links to Test 02. That result explicitly acknowledges different people and more than one visual change, so it does not isolate a cause.

## Project files, backups, and collaboration

### Move the latest file explicitly

1. Export the full project JSON from the tool you most recently used.
2. Open that latest JSON in the next Avalon tool.
3. Review the project ID, version, and module changes before replacement.
4. Download the current workspace as a backup if you need to keep it.
5. Confirm replacement, make your edits, and export a new latest JSON.

Unfamiliar tool entries present in an accepted snapshot are retained as inert JSON. This app checks their generic JSON safety and size, but does not validate or interpret their tool-specific meaning. It edits only its own `playtest` namespace and shared profile fields you explicitly change.

The import preview identifies current modules that are absent from the incoming file. A full replacement removes those absent modules from the active workspace. There is no automatic merging, background synchronization, or timestamp-based winner selection. Canceling, rejecting, or failing an import leaves the current workspace intact.

A valid shared project without a Playtest module is accepted after review, then receives an empty Playtest v1 module. An existing supported module is retained. An unsupported root schema or unsupported Playtest module version is refused.

Readable reports and CSV tables can be used alongside the Creator Guide or shared with collaborators. No report is automatically delivered to another tool. CSV and readable reports are exports; the supported structured import is the full project JSON.

### Browser save status

After committed edits, the app attempts browser autosave and reports success or failure. If saving fails, the work remains in the current page's memory and manual JSON export remains available. An un-restorable browser record can be downloaded as recovery text before replacement.

Browser storage may be blocked, cleared, or isolated by browser and file location. MDN states that storage behavior for directly opened `file:` URLs is undefined and may vary between browsers: [Window: localStorage property](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage), reviewed October 21, 2026.

Neither the downloaded HTML nor browser autosave is a substitute for an exported project JSON. Do not assume that work follows the HTML when it is moved, follows you to another browser, or survives clearing storage. Save an export before switching files or browsers.

## Payload schema reference

### Shared snapshot

The root envelope uses `format: "avalon.creator-project"` and `schemaVersion: 1`.

| Root field | Type and meaning |
|---|---|
| `format` | Literal string `avalon.creator-project` |
| `schemaVersion` | Integer `1` |
| `project` | Shared profile object described below |
| `tools` | Object containing tool namespaces; other tools remain inert JSON |

| Shared project field | Type |
|---|---|
| `id` | UUID string generated once |
| `name` | String, up to 300 characters |
| `platform`, `stage` | Strings, each up to 100 characters |
| `engine`, `genre`, `gameVersion` | Strings, each up to 200 characters |
| `targetAudience` | String, up to 3,000 characters |
| `targetDevices` | Array of up to 32 unique strings, each up to 100 characters |
| `designPillars` | Array of up to 32 unique strings, each up to 1,000 characters |
| `sessionLengthMinutes` | `null` or a nonnegative finite number, maximum 1,000,000 minutes |

The owned module is `tools.playtest`:

| Module field | Type |
|---|---|
| `moduleVersion` | Integer `1` |
| `updatedAt` | ISO 8601 timestamp with timezone, updated on committed Playtest changes |
| `payload` | Object with exactly the seven arrays below |

```json
{
  "testers": [],
  "tests": [],
  "sessions": [],
  "observations": [],
  "findings": [],
  "rules": [],
  "actions": []
}
```

All documented record fields are required in imported Playtest v1 records. Blank strings represent unknown or not-entered text. Numeric unknowns use `null`. Enum fields use their stated unknown value where supported. Unknown record fields in the owned module are rejected, rather than silently removed. Additional safe root/profile metadata and unfamiliar tool data are preserved without interpretation.

Imported numeric measurements must also be no greater than 9,007,199,254,740,991; the shared session-length field has the smaller limit shown above. Some entry controls apply narrower practical limits.

Record IDs are UUID strings and must be unique within their collection. References must resolve to existing records. Creation timestamps use ISO 8601 with a timezone. Calendar dates use `YYYY-MM-DD` or a blank string.

### `testers` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `alias` | String, maximum 120 characters; editable display name |
| `notes` | String, maximum 20,000 characters |

### `tests` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `title` | String, maximum 300 characters |
| `template` | `onboarding`, `core_loop`, `difficulty`, `multiplayer`, `controls`, `update`, or `custom` |
| `buildVersion`, `device`, `input`, `metricKey` | Strings, each maximum 200 characters |
| `startDate`, `endDate` | Calendar date or blank; a known end date cannot precede a known start date |
| `audience`, `question`, `hypothesis`, `task`, `successCriterion`, `recruitment` | Strings, each maximum 20,000 characters |
| `instructions`, `worksheet`, `behaviorQuestions`, `preferenceQuestions`, `notes` | Strings, each maximum 20,000 characters |
| `status` | `planned`, `running`, or `reviewed` |
| `createdAt` | ISO timestamp with timezone |

### `sessions` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `testId` | UUID referencing `tests.id` |
| `testerId` | UUID referencing `testers.id` |
| `date` | Calendar date or blank |
| `buildVersion`, `device`, `input` | Strings, each maximum 200 characters; actual session context |
| `status` | `planned`, `in_progress`, `completed`, or `incomplete` |
| `attempts` | `null` or a nonnegative safe integer |
| `completion` | `unknown`, `yes`, or `no` |
| `assistance` | `unknown`, `none`, `prompt`, or `guided` |
| `elapsedSeconds` | `null` or a nonnegative finite number |
| `startAt`, `endAt` | Blank or ISO timestamps with timezone; known end cannot precede known start |
| `behaviorAnswers`, `preferenceAnswers`, `notes` | Strings, each maximum 20,000 characters |
| `recordingUrl` | Blank or an absolute HTTP/HTTPS URL without credentials or whitespace; maximum 2,048 characters |
| `createdAt` | ISO timestamp with timezone |

### `observations` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `sessionId` | UUID referencing `sessions.id` |
| `kind` | `observation`, `quotation`, `interpretation`, `solution`, or `bug` |
| `text` | String, maximum 20,000 characters |
| `tags` | Array of up to 32 unique strings, each maximum 100 characters |
| `elapsedSeconds` | `null` or a nonnegative finite number; optional note marker |
| `createdAt` | ISO timestamp with timezone |

### `findings` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `testId` | UUID referencing `tests.id` |
| `title` | String, maximum 300 characters |
| `summary`, `explanation` | Strings, each maximum 20,000 characters |
| `severity` | `low`, `moderate`, `high`, or `critical` |
| `tag` | String, maximum 100 characters |
| `observationIds` | Array of unique UUID references to notes from this test |
| `sessionIds` | Array of unique UUID references to sessions from this test |
| `status` | `open`, `investigating`, or `resolved` |
| `createdAt` | ISO timestamp with timezone |

### `rules` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `name`, `needle` | Strings, each maximum 200 characters |
| `tag` | String, maximum 100 characters |
| `matchIn` | `all`, `observation`, `quotation`, `interpretation`, `solution`, or `bug` |
| `enabled` | Boolean; an enabled rule requires a nonblank literal phrase and tag |

### `actions` records

| Fields | Type or allowed values |
|---|---|
| `id` | UUID |
| `testId` | UUID referencing the originating test |
| `findingId` | `null` or UUID referencing a finding in that test |
| `suggestionKey`, `title` | Strings, each maximum 300 characters |
| `why`, `decisionReason`, `change`, `successMeasure`, `result` | Strings, each maximum 20,000 characters |
| `decision` | `pending`, `accepted`, or `rejected` |
| `nextTestId` | `null` or UUID referencing a different test |
| `createdAt` | ISO timestamp with timezone |

### Size and safety limits

The import limit is 5 MiB of JSON. Exports use readable formatting when it fits, and automatically use compact JSON when formatting would exceed the import limit. This keeps a supported project exportable and reimportable. Generic checks also limit nesting to 30 levels, visited JSON values to 200,000, and any individual string to 50,000 characters. Owned fields have the stricter limits shown above. Collection limits are 5,000 testers, 500 tests, 10,000 sessions, 20,000 observations, 5,000 findings, 500 rules, and 5,000 actions. Finding ID arrays allow at most 20,000 entries each.

Data must be ordinary JSON with finite numbers. Unsafe object keys `__proto__`, `prototype`, and `constructor` are rejected at any depth, including unfamiliar modules. Invalid IDs, duplicate record IDs, dangling links, cross-test evidence references, unsupported versions, and invalid dates are rejected before replacement.

Imported text is treated as data. Navigable recording links are restricted to HTTP and HTTPS. CSV fields are quoted, embedded quotation marks are escaped, and potentially active spreadsheet formula strings are prefixed with an apostrophe. The original values remain unchanged in JSON. CSV export is a collaboration format and is not a project backup.

## Why these implementation choices were made

| Decision | Reason for the chosen approach | Alternative 1 | Alternative 2 |
|---|---|---|---|
| One self-contained HTML app | Easy to distribute freely and use offline across responsive browser layouts, with no installation or recurring service requirement | A hosted web app would support accounts and centralized storage but add hosting, access, and service dependencies | A native app family would permit platform-specific behavior but require separate packaging, distribution, and maintenance |
| Creator-entered evidence with explicit tags and rules | Findings remain inspectable, linked to recorded sessions, and usable offline | Automated telemetry could measure events at scale but requires game instrumentation and still needs interpretation | An AI analysis service could assist with text patterns but adds model, privacy, cost, and verification dependencies |
| Explicit whole-project JSON transfer | Project identity and unfamiliar tool data remain visible and portable without an account system | Automatic synchronization would require a shared service and conflict-resolution design | Separate isolated files per tool would be simpler locally but make the shared project profile and foreign namespaces harder to preserve |
| Conservative comparison checks | Missing or changed definitions are exposed before a numerical delta is presented | Looser text matching could accept semantically equivalent wording but might also combine different tasks | Full statistical experiment tooling would need allocation, recruitment, measurement, and analysis capabilities beyond these observed session records |

## Sources reviewed

All sources below were opened and reviewed on **October 21, 2026**. Their summaries and the templates are written for this tool. No source establishes a universal pass rate for a small playtest.

| Source | What it informs |
|---|---|
| [Onboarding, Roblox Creator Hub](https://create.roblox.com/docs/production/game-design/onboarding) | Controls, core-loop understanding, and visible goals as useful onboarding questions |
| [Studio testing modes, Roblox Creator Hub](https://create.roblox.com/docs/studio/testing-modes) | Recording the actual solo, multiplayer, device, controller, or network test environment |
| [Steam Playtest, Steamworks Documentation](https://partner.steamgames.com/doc/features/playtest) | Steam Playtest is associated with a separate appID; creators arrange their own feedback collection |
| [Window: localStorage property, MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) | Browser-storage limitations, especially for directly opened local files |
| [Using moderated usability testing, GOV.UK Service Manual](https://www.gov.uk/service-manual/user-research/using-moderated-usability-testing) | Research questions, relevant participants, neutral task goals, and a consistent session guide |
| [Analyse a research session, GOV.UK Service Manual](https://www.gov.uk/service-manual/user-research/analyse-a-research-session) | Separating observations from interpretations, grouping evidence, and deciding actions |

## Version 1.0 change log

### Planning and sessions

- Added the branded start screen, clean blank start, and completed fictional example.
- Added the shared project profile and stable project identity.
- Added six editable research templates and a custom-question option.
- Added progressive planning forms for question, context, and session instructions.
- Added tester aliases with internal stable IDs and reusable tester records. New sessions default to creating a new tester; choosing an existing tester disables the new-alias field so an entered alias cannot be silently ignored.
- Added sessions with actual build/device/input context, statuses, task outcomes, assistance, attempts, optional timing, debrief answers, and optional recording links.
- Added separate observation, quotation, interpretation, solution, and bug notes. Editing another session field preserves unchanged timestamps, including fractional seconds.

### Review and decisions

- Added manual tags, editable literal matching rules, reviewed tag application, and reviewed finding grouping.
- Added stable findings with source-note/session references and creator-assigned severity.
- Added distinct-tester coverage, per-metric missing values, incomplete-session exclusions, repeated-session deduplication, and explicit calculation definitions.
- Added inspectable suggestions for recognized finding tags and missing-evidence messages.
- Added accepted/rejected/pending actions, decision reasons, defined changes, success measures, linked later tests, and written results.
- Added compatibility checks for ordinary before/after comparisons, with raw results and exposed differences.

### Portability and reporting

- Added the Avalon creator-project v1 envelope and Playtest module v1.
- Added validation before replacement, project/module previews, current-project backup, and explicit cancellation.
- Preserved unfamiliar tool data as inert JSON while refusing unsupported Playtest versions.
- Added browser autosave status and recovery behavior, manual JSON export/import, readable collaboration reports, and CSV exports.
- Added responsive layouts, keyboard focus treatment, and print-specific presentation. Corrected long-URL wrapping at 320 pixels and kept the file picker hidden until Open JSON is used.
- Added reviewed source guidance and a documented payload schema.

## Known limits

Physical phones, tablets, Safari, Firefox, assistive technologies, real games, game engines, and other Avalon tools have not been checked with this tool. No full screen-reader or accessibility audit has been done. No account, game distribution, telemetry, or automatic synchronization is built in.

## License

This tool is free and source available under the AmadOpenSource License 1.0 (see [LICENSE](../LICENSE)). Use it for anything, including paid work; what you make with it is yours. The tool itself may not be sold or turned into a paid product. Keep the license notice when you share or change it. Linked source pages keep their owners' rights.
