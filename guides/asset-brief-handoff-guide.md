# Avalon Asset Brief & Handoff Builder

**Avalon Partner · Captain Amado, streamer and community presenter**  
Version 1.0 · 21 October 2026

## Open the app

Open [`tools/asset-brief-handoff-builder.html`](../tools/asset-brief-handoff-builder.html) in a modern browser. This one file contains the entire application, including its styles, scripts, reference summaries, and examples. No installation, account, API key, internet connection, external font, CDN, build step, or backend is required for the core workflow.

The application file and your project data are separate. The HTML does not rewrite itself when you edit a brief. Use **Export JSON** to download the portable project file.

For this release, desktop, tablet, and phone support means responsive browser layouts in this HTML application. There are no separate native app or extension packages.

## Quick start

1. Choose **Explore the example** to see four filled production specifications, or **Start empty project** for your own work.
2. Open **Project profile** and enter the shared game name, engine, platform, audience, devices, game version, and design pillars.
3. In **Asset register**, choose **Add asset** and select a 3D model, rig, animation, 2D art, interface asset, sound effect, or music.
4. Work through the seven brief sections: purpose, specifications, references, dependencies, acceptance, handoff, and optional budget.
5. Use **Save brief** to commit the edit session. Ctrl+S or Command+S also saves the current edit session inside the app.
6. Open **Handoff outputs** to select the human brief, AI-ready instruction brief, or acceptance checklist. Download Markdown, copy it, or print it. The combined Markdown export includes all three outputs in one file.
7. Export the latest project JSON after meaningful work and before moving between tools or browsers.

### Try the dependency example

Open **Mossback sentinel**, go to **Specifications**, and change the target rig. Save the brief. Open **Mossback breathing idle** and inspect its dependency review flag.

The animation's declared rig is retained. Review it and decide what needs changing. Acknowledging the flag records that decision; the animation's acceptance criteria retain their own verification status.

## Included workflow

### Progressive asset briefs

Every asset has a purpose, audience, direction, context, required variations, completion definition, owner, version, due date, and production status.

Technical sections expose relevant fields:

| Asset type | Technical scope |
| --- | --- |
| 3D model | Scale and units, dimensions, pivot, collisions, attachments, rig choice, textures, materials, final formats, and creator-chosen performance budgets |
| Rig | Exact target rig/version, hierarchy and deformation requirements, scale, dimensions, pivot, collision/attachments, format, and test context |
| Animation | Named action, duration, optional authoring frame rate, loop behavior, root motion, transitions, exact rig compatibility, contacts, and export format |
| 2D art | Usage size, variations/frames, transparency, scaling, editable layers, color handling, and formats |
| Interface asset | Usage sizes, states, alpha edges, scaling/safe area, editable sources, themes, and formats |
| Sound effect | Duration, loop seam, channels, format/settings, playback context, intensity variations, and mix requirements |
| Music | Audio fields plus stems, arrangement, and musical transitions |

Unknown values remain unanswered. A numeric-looking specification may retain a planning expression such as “until the player exits.” Explicit number fields, including budget amounts and project session length, retain blank values as `null`.

### References, changes, and delivery

References retain URLs, source-record links or IDs, attribution, supplied license information, notes, and approval for creative direction. Creative approval does not establish permission to use the reference.

Dependencies carry an upstream asset UUID, a kind, and a note. Changes to production requirements propagate review flags to direct and downstream dependents. Rig changes and approved-reference changes receive specific reasons. Related assets are associations and do not propagate flags.

The handoff records editable sources, final exports, naming conventions, recipient, and implementation notes. Actual delivery records can contain filenames, versions, URLs or locations, roles, and notes. No binary assets are attached, inspected, uploaded, or delivered by this tool.

Revision requests record who asked, when, the requested change, status, and resolution. Saved history records changes. A production change advances the brief revision; administrative updates such as changing the owner or workflow status do not automatically invalidate production reviews.

### Requirements and verification

An acceptance criterion contains a requirement, method, and observable expected result. A reviewer decision separately records outcome, reviewer, evidence or explanation, timestamp, asset version, and brief revision.

- **Unverified:** no complete reviewer decision is recorded.
- **Reviewer pass / fail:** a creator-entered decision matches the saved brief revision and asset version.
- **Stale:** an older decision belongs to a different brief revision or version.
- **Accepted by owner:** a workflow status that does not pass individual criteria.

Reviewer identity and evidence are not authenticated by the HTML. A recorded filename, URL, or delivery status never establishes visual quality, audio quality, rig compatibility, engine performance, or rights clearance.

The HTML checks entered data: required field presence, references between asset records, revision freshness, unresolved requests, budget arithmetic, and scoped numeric planning checks. It does not analyze the meaning of a vague sentence or inspect an external asset.

### Optional budget and milestones

Each brief uses one explicit three-letter currency. A milestone includes a name, amount, due date, deliverable, and status. Amounts are user-entered allocations, not price benchmarks.

The known subtotal adds entered milestone amounts. If no amounts exist, the interface says so. A complete allocation requires every listed milestone amount. Unallocated budget remains unknown until the budget, currency, and complete milestone allocation are present. Explicit zero amounts remain zero. No exchange rates, taxes, fees, payments, or contract terms are inferred.

## Saving, importing, and moving projects

Browser autosave attempts to retain the committed workspace and in-progress edits. The header reports success or failure. Local-file browser storage behavior can vary; the browser's policy, private browsing, file location, or cleared storage can affect recovery. See [MDN: Window localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage), reviewed 21 October 2026.

**Keep the HTML and exported JSON. Browser storage and the downloaded HTML are not backups of one another.**

If an editor draft cannot be validated during recovery, a valid committed snapshot can still be restored. Rejected draft text is retained separately when storage permits and remains downloadable until explicitly cleared. When that preservation cannot be written, the app avoids silently overwriting the original recovery with a later autosave.

Import is a full replacement preview. It shows current and incoming names, UUIDs, game versions, asset counts, module differences, and modules absent from the incoming file. It offers a current backup, including pending edits, before replacement. Canceling or refusing an import leaves the workspace unchanged.

Use your **latest project JSON** when moving between Avalon creator tools. This is explicit file transfer. There is no automatic synchronization, module mapping, delivery to another app, automatic merge, or timestamp-based winner selection. A matching name does not establish project identity. Explicit project duplication generates a new project UUID.

## Portable data contract

The exact root format is `avalon.creator-project`, schema version `1`. The shared `project` object contains:

`id`, `name`, `platform`, `engine`, `genre`, `targetAudience`, `targetDevices`, `stage`, `gameVersion`, `designPillars`, `sessionLengthMinutes`.

The project UUID is generated once and retained across saves. The two plural profile fields are string arrays. Session length is a number of minutes or `null`; the remaining profile fields are strings.

This app owns only:

```json
{
  "tools": {
    "asset_briefs": {
      "moduleVersion": 1,
      "updatedAt": "ACTUAL_ISO_8601_TIMESTAMP",
      "payload": {
        "assets": []
      }
    }
  }
}
```

Each asset has:

| Field group | Fields and meaning |
| --- | --- |
| Identity and workflow | `id`, `type`, `name`, `code`, `version`, `owner`, `dueDate`, `status` |
| Common requirements | `purpose`, `audience`, `direction`, `context`, `variations`, `completion`, `engine`, `platform` |
| Technical requirements | `specs`: string-valued fields; unfamiliar safe string keys are retained, with nonempty values included in reports |
| Relationships | `relatedAssets`: UUIDs; `dependencies`: `assetId`, `kind`, `note` |
| References | `id`, `label`, `url`, `sourceRecord`, `attribution`, `license`, `notes`, `approved` |
| Acceptance | `id`, `requirement`, `method`, `expected`, and `review` with `status`, `reviewer`, `evidence`, `checkedAt`, `version`, `assetRevision` |
| Revision requests | `id`, `requestedAt`, `by`, `note`, `status`, `resolution` |
| Deliveries | `id`, `kind`, `name`, `url`, `version`, `notes` |
| Handoff | `sourceFiles`, `finalExports`, `naming`, `implementation`, `recipient` |
| Budget | `currency`, `total`, `scope`, `assumptions`, `milestones` |
| Milestones | `id`, `name`, `amount`, `dueDate`, `deliverable`, `status` |
| Dependency reviews | `id`, `sourceId`, `reason`, `createdAt`, `status`, `reviewer`, `note`, `resolvedAt` |
| History | `id`, `at`, `by`, `summary` |
| Revision metadata | `createdAt`, `updatedAt`, `revision` |

Supported asset type values are `model`, `rig`, `animation`, `art2d`, `interface`, `sfx`, and `music`. Production statuses are `draft`, `ready`, `in_progress`, `submitted`, `revision`, and `accepted`. Dependency kinds are `rig`, `style`, and `general`.

Budget totals and milestone amounts are nonnegative finite numbers or `null`. Due dates use `YYYY-MM-DD` or an empty string. Record timestamps use ISO 8601. New reviewer records begin unverified.

Safe unfamiliar properties and foreign modules remain inert JSON through export. Their specialized meaning is not validated. Unsupported root schemas and unsupported versions of `asset_briefs` are refused without resetting their payloads. No specialized CSV or single-record import mapping is implemented.

### Limits and safety

- Project import: 5 MiB UTF-8 JSON, depth 30, 150,000 values, and 100,000 characters per string.
- Up to 250 assets and 200 records per asset collection, including history. A full history causes a save refusal rather than silent removal.
- Unsafe object keys are rejected recursively; imported content is treated as data.
- Only HTTP and HTTPS URLs become navigable links. Other locations remain text.
- CSV cells are escaped and formula prefixes are neutralized. JSON retains the original values.
- Markdown and print are collaboration reports; CSV is a register summary. JSON is the editable project snapshot.

## Research record

All sources below were opened and reviewed on **21 October 2026**. The app includes concise source summaries and links. It performs no live refresh.

| Source | Use in this release |
| --- | --- |
| [3D art in Roblox](https://create.roblox.com/docs/art) | Workflow overview and asset-category scope |
| [General specifications](https://create.roblox.com/docs/art/modeling/specifications) | General mesh, rig, and animation-export requirements |
| [Export settings](https://create.roblox.com/docs/art/modeling/export-requirements) | Documented Blender/Maya FBX workflow |
| [Importer](https://create.roblox.com/docs/studio/importer) | Supported import paths and the need to verify imported structure |
| [Audio assets](https://create.roblox.com/docs/audio/assets) | Scoped audio import requirements and declared-duration comparison |
| [Animation Editor](https://create.roblox.com/docs/animation/editor) | Rig-dependent animation authoring and loop review context |
| [UI 9-slice design](https://create.roblox.com/docs/ui/9-slice) | Optional scaling guidance for interface imagery |
| [Texture specifications](https://create.roblox.com/docs/art/modeling/texture-specifications) | Texture guidance, including its unresolved resolution inconsistency |
| [MDN localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) | Browser storage limitations and accurate recovery messaging |

The general mesh ceiling is shown with its per-mesh scope, separately from a creator's performance budget. No universal triangle budget, texture resolution, loudness target, or animation timing is imposed. The conflicting texture-resolution statements are disclosed rather than turned into a single enforced maximum. Example budgets and settings are fictional project choices.

## Known limits

Physical phones and tablets, Safari, Firefox, native applications, browser extensions, actual Roblox Studio imports, external asset files, visual and audio quality, live links, rights clearance, authenticated reviewer identity, cloud synchronization, and integrations with other tools have not been checked. These capabilities are not represented as implemented.

## Major decisions and alternatives

| Decision | Why it was chosen | Two alternatives considered |
| --- | --- | --- |
| Single self-contained HTML | Easy free distribution, responsive use, and offline operation | A spreadsheet would simplify tabular entry but weaken progressive forms and change tracking. A hosted app could add collaboration but would require hosting and an account/data architecture. |
| Explicit reviewer evidence | Preserves the difference between a request, a delivery record, and a reviewed outcome | An automatic quality score would imply inspections this HTML cannot perform. Engine plugins could provide real checks but would require separate implementations and testing. |
| Explicit JSON replacement preview | Preserves project identity and unfamiliar module data while making replacement reviewable | Automatic merging could create contradictory requirements. Picking the newest timestamp could silently discard intentional changes. |

## Distribution and license

Share the HTML file directly. This tool is free and source available under the AmadOpenSource License 1.0 (see [LICENSE](../LICENSE)). Use it for anything, including paid work; what you make with it is yours. The tool itself may not be sold or turned into a paid product. Keep the license notice when you share or change it. Source documentation remains the property of its respective owners; no third-party fonts, images, libraries, or production asset files are bundled.

The tool is branded Avalon Partner and Captain Amado. It is an independent creator tool and is not affiliated with or endorsed by Roblox.
