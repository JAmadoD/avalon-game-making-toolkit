# Avalon Game Balance & Economy Simulator

**Avalon Partner** · **Captain Amado**, streamer and community presenter  
Version 1.0.0 · Released 21 October 2026

## Start here

Open [`tools/game-balance-economy-simulator.html`](../tools/game-balance-economy-simulator.html) in a modern browser. The complete app, its styles, calculation engine, example models, source notes, and project-file handling are inside this one file. It works offline. No installation, login, paid API, external font, CDN, server, or build step is needed to use it.

Choose the **Roblox round game**, **Collection & crafting**, or **Progression RPG** example to learn the controls. Choose **Empty project** to use the four-step guided setup. The examples are invented teaching models, not Roblox benchmarks or recommended grind durations.

For the fastest first test:

1. Open the Roblox round example. It starts in **My tuning**, with an independent protected baseline.
2. Open **Rewards & upgrades**. The 1,200-coin movement upgrade starts at 30 completed rounds and 90 minutes.
3. Change the base reward from 40 to 80 coins per round. The working scenario now needs 15 rounds and 45 minutes. Its baseline retains 40 coins, 30 rounds, and 90 minutes.
4. Open **Compare scenarios** and compare the selected scenario with the baseline.
5. Click **Export project**. Keep this latest JSON file as the editable record of your work.

The HTML is the tool. Your downloaded JSON is the project. Browser autosave and the HTML file are not backups of one another.

## What the workspace does

| Module | Inputs and decisions | Results |
| --- | --- | --- |
| Guided setup | Shared game profile, audience, devices, design pillars, player goal, timing, wallet, first reward and target | A model with your own pacing goals and explicit unknowns |
| Rewards & upgrades | Fixed reward, starting wallet, bonuses, round cost, cap, waiting, named upgrade prices | Whole completed rounds, elapsed minutes, reachability, and goal comparisons |
| Currency flows | Period, extra earning/spending actions, order of purchases, repeat purchases, event multiplier, optional purchased grant and source boost | Ordinary/event/purchased wallet histories, source and sink totals, cap losses, skipped payments, and purchase timing |
| XP & levels | Linear or geometric per-level growth, custom per-level requirements, or custom cumulative thresholds | Transition XP, cumulative XP, remaining XP, whole rounds and elapsed minutes |
| Drops & chance | Independent outcomes, mutually exclusive outcomes, or a single-target hard guarantee; target, attempt budget, seed and sample count | Expected value, expected attempts, exact success probability, quantiles, and separate seeded sampling |
| Crafting | Items, inventory, ingredient quantities, recipe output batches, target quantity | Aggregated shared demand, inventory use, gathering shortages, whole craft batches and surplus |
| Combat | Target HP, damage, attack rate, first-hit timing, accuracy assumption, magazine, reload and cooldown | Deterministic attacks needed, defeat time, reload count, burst DPS and sustained DPS |
| Compare scenarios | Two named scenarios and a balance, XP or probability chart measure | Side-by-side numbers, editable charts and accessible data tables |
| Report & sources | Current model and comparison choices | A readable tuning report, input CSV, result CSV, optional AI prompt, source notes and print/PDF layout |

Edit the fields to update calculations and charts. Large record lists have search controls. Upgrades and action sinks can be reordered. Deletion asks for confirmation. Crafting items still used by recipes cannot be deleted until those references are removed or changed.

### Use a baseline deliberately

The supplied examples contain a protected baseline and a separate editable scenario. **Duplicate to tune** always creates independent scenario data.

**Save baseline** copies the selected scenario and protects that copy. Your working scenario remains editable. If a baseline already exists, it remains in the project as an ordinary scenario with its numbers preserved. Only the newly designated baseline is protected. Deleting the protected baseline requires an explicit confirmation.

The shared project profile belongs to the entire project. Explicit profile edits apply across its scenarios. Names label projects and scenarios; a matching name does not mean two projects share identity.

## Read the calculations correctly

The workspace distinguishes calculation, assumption, model observation, and suggestion. It does not claim to observe player behavior, read analytics, integrate with an engine, or infer willingness to pay.

### Fixed rewards and whole rounds

Gross reward is:

`base reward × (1 + bonus percentage / 100) + flat bonus`

Net fixed reward subtracts the round cost. A reachable target above the starting wallet uses ceiling arithmetic:

`completed rounds = ceiling((price - capped starting balance) / net fixed reward)`

Each target in this module is evaluated independently. Buying one target does not consume another target's independent starting wallet. The **Currency flows** module models actual sequential spending.

Time is:

`completed rounds × (round duration + waiting before each round)`

Waiting is charged once for every completed round, including the first. Enter zero to exclude it. An already affordable target takes zero rounds and zero minutes in this independent affordability calculation. Currency-flow purchases occur at the end of a completed round, including when starting resources could already cover the price.

The cap applies before the round cost. That matters: a 100-coin cap with a 10-coin round cost leaves at most 90 coins at the end of a paid round. A 95-coin target may therefore be unreachable even though its price is below the cap.

Zero earnings, nonpositive net earning, unreachable cap-bound targets, missing timing, and unsupported numeric ranges are reported explicitly. Decimal currency arithmetic is handled internally so values such as 0.28 / 0.01 do not gain an extra round through binary rounding.

### Currency simulation order

Each modeled round follows this order:

1. Add the base reward, bonuses, and extra source actions, applying the selected path's source multiplier.
2. Apply the wallet cap and record discarded overflow.
3. Attempt the round cost, then listed action sinks in their displayed order.
4. Make enabled upgrade purchases according to the selected spending rule.

Each action's per-round amount is `amount × occurrences`. A sink row is one aggregated payment. If the wallet cannot pay that total, the whole payment is skipped and recorded. The model allows no debt or partial payment. A real game may instead block the action, which is a different behavior to test.

**Ordered** spending waits for the first unowned target. **Cheapest first** considers prices in ascending order. Repeat purchases are limited to once per target per completed round. With repeats off, a target can be bought once during the whole period. Zero-price targets do not create infinite purchase loops.

The event multiplier affects all currency sources. The optional purchased path adds a starting grant and a source boost separately from the event path. These are virtual benefits with no real-world price conversion. A modeled surplus is not evidence of market inflation or a forecast of revenue.

### XP

The model starting level is the zero-XP anchor. Existing XP is measured from that anchor, not from the start of the player's current level.

Per-level requirements specify additional XP for one transition. Cumulative thresholds specify the total from the anchor. Custom cumulative values must not decrease. Changing the model type preserves entered custom rows, so review the meaning of those values when switching between modes.

The XP module does not automatically take XP from combat or crafting. Inputs remain explicit and independent.

### Drop probabilities

For independent attempts at a fixed target probability `p`:

`P(at least one success within n attempts) = 1 - (1 - p)^n`

`Expected attempts through first success = 1 / p`, for positive `p`.

At a 10% chance, two attempts give a 19% probability of at least one success. Ten expected attempts do not guarantee success on attempt ten.

Independent outcome rows may award several items on one attempt. Mutually exclusive rows award at most one listed outcome; their total must be at most 100%. Any remainder is explicitly a no-item outcome. Invalid totals are rejected by the calculator and are never normalized silently.

The hard-guarantee model supports exactly one target row. It starts with a fresh counter, guarantees success by the specified limit, and assumes reset after success. First-attempt expected value and long-run value under resets are labeled separately. Soft pity, shared pity, duplicate protection, without-replacement draws and conditional drop chains are outside this version.

Sampling is seeded and reproducible. It samples only the selected target's first-success behavior, not a complete multi-item inventory. Sample observations are separate from exact formula results. Set the sample count to zero for exact results only. Repeatability is not a confidence claim about a real game's players.

### Crafting

The calculator follows the selected target's dependency graph. It aggregates shared ingredient demand before consuming inventory and rounding batches. Existing inventory is used once, avoiding double counting when several branches require the same material.

An item without ingredients is a gathered resource. An item with ingredients is crafted recursively. Recipe cycles require correction, even when current inventory covers the target. Items outside the selected target graph are not evaluated as part of that calculation.

Recipes assume deterministic 100% yield. Crafting failures, byproducts, stations, crafting time and currency fees are outside the model.

### Combat

The attack interval is the slower of the entered attack rate and cooldown. First hit is either immediate at time zero or delayed by one full interval. Reload duration is an additional sequential delay on top of the regular interval before the next magazine.

Accuracy below 100% scales damage on every attack. For example, 20 damage at 50% accuracy becomes a deterministic 10 damage per attack. This is a comparison assumption, not simulated misses or expected real combat time. DPS and deterministic defeat time do not predict win rates. Movement, armor, critical hits, healing, player reactions, range and network delay are not modeled.

## Keep, transfer, and share your work

### Project JSON

**Export project** downloads the complete shared snapshot, including unfamiliar tool entries. The format is `avalon.creator-project`, root `schemaVersion: 1`, with this tool's data in `tools.balance` and `moduleVersion: 1`.

The project UUID is generated once and retained across saves. **Duplicate project with a new identity** creates a separate project UUID. The ordinary profile form does not let users edit identity directly.

Import previews show project identity, game version, module changes, and current modules absent from the incoming file. Export the current backup from that dialog if you need it, then explicitly replace or cancel. The app does not merge divergent snapshots or choose a winner using timestamps.

An absent balance module receives a new blank balance module after import approval. An existing supported balance module is loaded intact. Unsupported root or balance versions are refused. Unfamiliar modules and versions remain inert JSON and are preserved without tool-specific interpretation.

Move your **latest project file** manually between creator tools. This release does not synchronize data, deliver it to other tools, or automatically interpret unfamiliar modules.

### Browser autosave

The app attempts local browser autosave and reports actual success or failure. If storage is blocked, the calculators remain usable and manual export still works. Local-file storage behavior varies by browser. Moving the HTML, changing browsers, clearing storage, and private browsing can affect access to saved data.

Do not rely on the browser copy as your only backup. Keep exported project JSON before important changes or transfers. The standalone HTML file does not automatically rewrite itself with your edits.

### Collaboration exports

**Download tuning report** creates a readable standalone HTML report with active inputs, scenario comparison, derived results, assumptions, formulas and reviewed sources. **Print / save PDF** uses a landscape print layout for wide tables. Reports include the complete active input appendix and can span many pages; the HTML report is convenient for digital sharing.

**Input tables CSV** and **Results CSV** include every scenario with stable field paths, units and value states. Long result histories are kept in the result export even when on-screen and printable tables use a labeled, evenly spaced display sample. CSV text that could be treated as a spreadsheet formula is prefixed defensively; original JSON is not rewritten. This version exports CSV and does not import specialized CSV records.

**Prompt for my AI** downloads a text prompt and the active inputs. It performs no AI call and uploads nothing automatically. Use it only if you choose to pass the content to your own AI tool.

## Sources

All sources below were opened and read on **21 October 2026**. The app includes concise original explanations, links, review dates and limitations. These are release review dates, not a claim that the offline file checks future documentation changes.

1. Roblox Creator Hub, [Balance virtual economies](https://create.roblox.com/docs/production/game-design/balance-virtual-economies).
2. Roblox Creator Hub, [Economy events](https://create.roblox.com/docs/production/analytics/economy-events).
3. MDN Web Docs, [Window: localStorage property](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage).
4. NIST/SEMATECH, [Binomial Distribution](https://www.itl.nist.gov/div898/handbook/eda/section3/eda366i.htm).
5. ProbabilityCourse, [Special Distributions](https://www.probabilitycourse.com/chapter3/3_1_5_special_discrete_distr.php).
6. ProbabilityCourse, [Expectation](https://www.probabilitycourse.com/chapter3/3_2_2_expectation.php).
7. Roblox Creator Hub, [Paid random items policy guidelines](https://create.roblox.com/docs/production/monetization/paid-random-items).

Roblox's current guidance informs the source/sink distinctions and the contextual paid-random note. Probability formulas are implemented independently and checked with numerical examples. The tool does not implement Roblox analytics, PolicyService or an engine connection.

## Worked examples

These cases show what the calculator returns for simple inputs.

| Case | Result |
| --- | --- |
| Start at 0 coins; price 1,200; earn 40 after each completed 3-minute round; no waiting | 30 rounds and 90 minutes |
| Zero earning with a positive target above the starting balance | Unattainable |
| Fixed independent 10% chance across two attempts | 19% probability of at least one success |
| Mutually exclusive probabilities totaling 120% | Correction required; no normalization |
| Edit a working scenario | Saved baseline retains the same data |

## Practical limits

This release supports up to 12 scenarios, 100 records in most input lists, 20 combat attacks, level numbers through 100, 10,000 modeled rounds, 10,000 attempt horizons and 10,000 sampled runs. JSON imports are limited to 5 MiB with nesting, text, record and numeric limits. Economy simulations have a bounded workload. These limits and unsupported numeric ranges produce explicit messages.

The tool has not been checked on physical phones, tablets, Safari, Firefox, Roblox Studio, game engines or physical printers.

Probability and displayed timing calculations use browser floating-point numbers. Exact decimal arithmetic is used for the relevant accumulation and affordability operations, but the public JSON values are ordinary numbers. This is not an arbitrary-precision scientific package.

## Why this implementation

The selected approach is a self-contained browser app with separate input data, calculation logic and display code embedded into the deliverable. It supports responsive forms, independent scenarios, charts, offline calculations and careful file transfers while remaining easy to distribute.

Two alternatives were considered:

| Alternative | Useful strengths | Tradeoff for this brief |
| --- | --- | --- |
| Spreadsheet workbook | Familiar bulk row editing and visible cell formulas | Guided navigation, protected scenario workflows, safe snapshot transfer and responsive phone use require more work from the creator |
| Hosted application with accounts and a database | Shared team access, permissions and online collaboration | Introduces hosting, accounts and online service dependencies beyond the requested offline single-file tool |

## License

This tool is free and source available under the AmadOpenSource License 1.0 (see [LICENSE](../LICENSE)). Use it for anything, including paid work; what you make with it is yours. The tool itself may not be sold or turned into a paid product. Keep the license notice when you share or change it. Linked publications retain their own rights. This tool is not affiliated with or endorsed by Roblox.
