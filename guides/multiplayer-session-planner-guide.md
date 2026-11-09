# Avalon Multiplayer Session Planner

**Version 1.0.0 | Sources reviewed 21 October 2026**

Presented by **Avalon Partner** and **Captain Amado, streamer and community presenter**.

The tool is [`tools/multiplayer-session-planner.html`](../tools/multiplayer-session-planner.html). It is a complete, self-contained browser app with embedded CSS, JavaScript, examples and documentation. It needs no installation, build step, account, backend, external font, CDN or paid API. Its core functions work offline.

## Start here

1. Open the HTML file in a browser. A desktop browser is the easiest place to complete the longer forms; the layout also adapts to tablet and phone browser widths.
2. Choose **Create an empty project** or open one of the three completed examples. Review and apply the proposed workspace before editing.
3. Complete **Project profile** and **Session rules**. Leave uncertain numbers blank. Blank means unknown; zero means a known, intentional zero.
4. Edit **Session flow**, then open **Scenarios**. Expand **Edit the current server and event** to enter local populations, teams, the incoming party, elapsed time and the departure event.
5. Inspect the resulting actions and decisions. Build an individual **Player timeline**, marking each duration as an assumption, an observation or unknown.
6. Use **Decisions & tests** to record owners, decisions, dependencies and actual game-test evidence.
7. Choose **Export project** for the portable JSON snapshot. Open **Design brief** for readable report downloads and printing.

## What is included

### Three complete design examples

| Example | Design | Focus |
| --- | --- | --- |
| Lantern Party | Roblox casual party minigames | Four-player minimum, practice while waiting, spectator late joins and whole-party waiting. |
| Vaultbound Expedition | Roblox cooperative dungeon | Two-to-four-player roster, checkpoint entry, paused recovery and reconnect reservations. |
| Signal Clash | Engine-neutral team objective match | Teams start 3 / 2; a departure exposes an actual 3 / 1 roster and a separate proposed 2 / 2 rebalance. |

All example numbers are illustrative designer assumptions. No example playtest is marked as performed.

### Eleven scenario cards

The planner generates one-player, two-player, uneven-team, nearly-full-server, oversized-party, late-join, departure, elimination, disconnect and empty-server cases, plus a custom case using the current server inputs.

Each card explains its inputs, calculation or assumption basis, available actions, blocked or conditional progress, affected populations and unresolved decisions. These are independent scenario probes, not a chronological simulation. Running a scenario does not change the saved server population.

The fixed oversized-party case always tests three incoming members against two open slots, or fewer if the configured server capacity is below two. The custom case separately evaluates the entered party size against the actual entered capacity and match rules.

### Editable states, transitions and timelines

The six base states are empty server, waiting lobby, ready countdown, active round, results and recovery. Their labels and descriptions are editable. Custom states and transitions can be added. A referenced custom state cannot be deleted until its transitions are updated or removed.

Every transition has a condition and outcomes for the match roster, non-roster spectators, local queue, party members, disconnected members and people on other servers. Free-text conditions are documentation. They do not execute or override the structured numerical rules.

A player timeline is an independently editable sequence. It reports main-match play, practice, total duration, time before first play, the longest interval outside main-match play and participation against creator-set goals. Unknown durations propagate to the affected totals. Updating a rule does not silently rewrite an existing timeline.

## Count people once

| Field | Meaning |
| --- | --- |
| Connected match roster | Includes eliminated players who still hold roster seats. |
| Eliminated roster members | A subset of the connected roster, not an additional population. |
| Non-roster spectators | Connected viewers without a match roster seat. |
| Eligible local queue | Connected players waiting for selection in this server. |
| Ready players | A subset of that local queue. All-ready selection uses only ready players. |
| Held reconnect seats | Logical seats for offline roster members; not connected or actively playing people. |
| Incoming party | A hypothetical external group that is not included in current occupancy before admission. |
| Players on other servers | Context only; excluded from local capacity, eligibility and wait calculations. |

Connected occupancy is roster plus non-roster spectators plus local queue. Server admission capacity also subtracts reconnect reservations. Match capacity and server capacity are separate checks.

## Saving and file transfer

The app attempts browser autosave and reports whether it succeeds. Failure leaves editing and manual JSON export available. Save feedback is visible on phone layouts too.

**The HTML contains the application. The JSON export contains your entered project.** Downloading or moving the HTML does not copy a browser's saved project data. Browser storage may be denied, vary for local files, disappear when storage is cleared, or be unavailable in another browser. A requested download should be checked in the browser's downloads list.

Move the **latest project JSON file** between compatible creator tools. This is explicit file transfer, with no automatic synchronization or delivery.

The shared envelope is `avalon.creator-project`, root `schemaVersion: 1`. The project UUID is generated once and retained through edits, renames and saves. Explicit duplication creates a new UUID. A matching name is not identity.

This app owns `tools.multiplayer_sessions`, with `moduleVersion: 1`, a valid UTC ISO `updatedAt` timestamp and its documented payload. It changes shared-profile fields only when the creator edits them. Unfamiliar tool entries and versions remain inert JSON in full exports; their tool-specific meaning is not validated.

Import validates the envelope, JSON safety and supported module schema before offering replacement. The preview shows identity, game version, module changes and current modules absent from the incoming file. A current-project backup download is offered. Invalid, unsupported and canceled imports leave the current workspace intact. Snapshots are not automatically merged or ranked by timestamps.

Import limits and the complete payload field guide are included under **Sources & guide**. Unsupported own-module or root versions are refused. Specialized CSV/record import is not implemented.

## Export options

| Control | Deliverable |
| --- | --- |
| Export project | Full portable JSON snapshot, including retained foreign modules. |
| Download report HTML | Standalone readable design brief with its own responsive and print styles. |
| Download Markdown | Text report for collaborators and project documentation. |
| Print / save as PDF | Complete design report through the browser's print function. |
| Export table CSV | Transition conditions and all affected-group outcomes. |
| Export matrix CSV | Scenario inputs, outcomes, actions and decisions. |
| Export checklist CSV | Playtest procedures, expected behavior and recorded evidence. |
| Export AI review prompt | Optional text for the creator's own AI. It does not call an AI service. |

CSV exports quote and escape fields and protect formula-like values from spreadsheet execution. Original values remain unchanged in JSON. Imported markup, notes, filenames and other text are rendered as data, not executable content.

## Worked examples

These cases show how the planner handles common edge cases.

| Case | Behavior |
| --- | --- |
| Two available players, minimum four | Normal match remains blocked. Practice and solo activity do not lower that minimum. An explicitly reduced minimum can permit a smaller roster only when the remaining team and readiness guards also pass. |
| Party of three, two open slots | Wait policy admits zero; split policy requires explicit scenario consent before admitting two and leaving one outside; routing is an unimplemented design dependency. |
| Mid-round departure and late join | Removing a player from the smaller team of 3 / 2 yields an actual 3 / 1 roster. A 2 / 2 rebalance is a separate proposal. A spectator-only late join does not silently repair the team. |

## Known limits

The planner has not been checked on physical iPhone, iPad or Android devices, or in Safari, Firefox and other browser engines. No actual Roblox Studio project, published Roblox experience, game server, matchmaking service, teleport, bot implementation or reconnect system has been tested with it. The layout adapts to narrow screens, but that is not device or game-engine compatibility certification.

## Change log: 1.0.0

- Built the complete offline app, shared-project envelope, three example projects, rules, editable state model, scenario lab, timelines, decisions, dependency records, playtest checklist and report exports.
- Separated server admission, match admission, roster membership, elimination, queues, party membership, reconnect reservations and other-server populations.
- Corrected all-ready selection to choose a legal ready subset while preserving unready and overflow players in the queue.
- Added strict calendar validation for imported module timestamps and preserved unknown values through saves and imports.
- Added actual custom-party admission checks alongside the fixed three-into-two acceptance scenario.
- Added logical match-capacity conflict checks and prevented empty rosters from promising a nonexistent match to watch.
- Kept actual post-departure teams distinct from proposed recovery compositions.
- Added visible phone autosave/error feedback and preserved manual export during storage failures.
- Made late-join timeline templates policy-aware. Checkpoint and respawn delays remain unknown without explicit evidence or assumptions.
- Grouped repeated unresolved findings in reports without dropping unique actions or reasons.
- Escaped imported text, protected CSV exports from spreadsheet formulas, rejected unsafe imports, and kept offline operation and responsive/print layouts.

## Major implementation choices

| Chosen approach | Why | Two alternatives considered |
| --- | --- | --- |
| One self-contained HTML app | Can be handed out free and opened offline with no account or infrastructure. | A hosted application would add hosting and synchronization requirements. A spreadsheet would make the role/transition workflow and guided scenario explanations less direct. |
| Deterministic scenario calculations | Results are reproducible and expose the inputs and missing decisions. | Stochastic queues need arrival, departure, routing and party assumptions that are not available. A narrative-only checklist would not catch numerical capacity or team contradictions. |
| Explicit latest-file transfer | Preserves shared identity and foreign tool data while letting the creator review replacement. | Automatic synchronization needs shared infrastructure. Timestamp-based merging can choose the wrong divergent snapshot. |

## Primary sources reviewed

All four pages were opened and reviewed on **21 October 2026**. These are source-review dates, not publication dates.

- [Client-server runtime, Roblox Creator Hub](https://create.roblox.com/docs/projects/client-server): authoritative server state and connected-client scope.
- [Studio testing modes, Roblox Creator Hub](https://create.roblox.com/docs/studio/testing-modes): multi-client, party, device and network testing guidance.
- [Teleport between places, Roblox Creator Hub](https://create.roblox.com/docs/projects/teleport): published-client testing and explicit teleport-failure handling.
- [Window: localStorage property, MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage): storage denial and browser-dependent behavior for local files.

The app does not infer a real arrival rate or expected wait from concurrent-player counts. Conditional phase timing is not a queue forecast. Bots, routing, reservations, checkpoint admission and engine integration remain implementation dependencies until the creator implements and tests them in the game.

## License

This tool is free and source available under the AmadOpenSource License 1.0 (see [LICENSE](../LICENSE)). Use it for anything, including paid work; what you make with it is yours. The tool itself may not be sold or turned into a paid product. Keep the license notice when you share or change it. No third-party runtime libraries, external fonts or imagery are bundled. Linked source pages retain their owners' rights.
