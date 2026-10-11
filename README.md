# Spearhead AI for OpenRA Red Alert

An experimental community bot developed through human spectator feedback, C# changes, controlled scenarios and full-game benchmarks, with assistance from OpenAI Codex. This is an independent project, not an official OpenRA or OpenAI release.

## Requirements and installation

Windows; **OpenRA release-20250330** with the Red Alert game assets already installed. Other versions are not yet supported by this package.

1. Download the release ZIP and extract the whole folder.
2. Open PowerShell in that folder and run `./Start-Spearhead.ps1 -EngineDir "C:/Program Files/OpenRA"` (substitute your installation path).
3. In the separate Spearhead Red Alert menu, create a skirmish and select **Spearhead AI** from the bot list. Original bots remain available for comparison.

The launcher loads this mod beside the existing installation. It does not replace stock Red Alert files. All participants in a multiplayer game need the same mod. It is not added to the stock Red Alert menu unless that menu is launched with this mod.

**Normal starts:** this user package excludes the test-world rules, automatic construction-yard deployment and free power plant/barracks/refinery. Lobby starting-unit settings apply. The benchmark below used the faster test start, so it does not establish the same win rate under ordinary starting conditions.

## Features

- Scouting and remembered contacts instead of deliberately querying every hidden enemy as an attack target; GPS revelation is used when available.
- More early exploration: two outward scouts plus eligible idle units exploring outward near home, with recall on threats and release for larger armies. The extra scouting is new and not yet demonstrated to improve overall win rate.
- Strategy reacts to observed threats, economic pressure and opportunities; coordinated attacks, regrouping and route/flank assessment.
- MCV expansion and rebuilding, reserving funds for expansion, support for threatened economic bases and MCV escorts.
- Engineers capture reachable neutral buildings, avoid unsafe routes and retry later; opportunistic APC engineer raids against suitable targets.
- Unit targeting considers usable weapons, effectiveness, range and worthwhile vulnerable targets; infantry under fire avoid the extra movement allowance; engineer interception gets special attention.
- Preserve valuable veterans when practical; aircraft rearming and anti-air responses; safer technology-building placement.
- Naval scouting, shore bombardment by cruisers/missile submarines, escort/recovery behavior and checks on useful naval access.
- Decision, attack, economy and actor telemetry in the development harness, including coordinates and expansion/refinery placement diagnostics.

These are implemented behaviors, not guarantees that every map, route or unit combination is handled optimally. Original opponent bots may use different information rules. We do not claim perfect human-level fog-of-war fairness across every inherited engine behavior.

## Test snapshot — 11 October 2026

**40/40 completed: 31 wins, 9 losses (77.5%).** This is a mixed-version development total, not the win rate of the downloadable version.

| AI revision | Completed | Wins | Losses |
| --- | ---: | ---: | ---: |
| spearhead-recovery | 12 | 9 | 3 |
| spearhead-economy | 24 | 18 | 6 |
| spearhead-recon-v2 | 4 | 4 | 0 |

The schedule covers original Rush, Normal, Turtle and Naval bots, maps including Polar Disorder, Warwind, Crossfire and the custom Bay of Pigs remake, Allied/Soviet factions and swapped starts. See [test data](docs/benchmark-snapshot.csv) and [methodology](docs/TESTING.md). One loss was explicitly confirmed by the user after closing a spectator match; its provenance is retained. Remaining matches are not counted. Some time-limit results can be assessed using economic and army advantages; this is distinct from an engine-declared win.

The newest revision has only the completed rows shown above. Earlier revisions cannot be treated as evidence for every newest feature. Controlled scouting tests were stopped at the user's request; their mixed results do not prove improved resistance to Rush.

## How it was built

Development started from OpenRA's existing bot modules, then added C# behavior and YAML configuration. A human watched games and identified issues such as delayed expansion, aimless movement, dangerous infantry attacks, inaccessible capture targets and inactive ships. Codex assisted with implementation, compilation, instrumentation and test analysis.

This snapshot contains **60 C# files and 7,264 C# lines**, including inherited/adapted bot code, logging and scenario fixtures. These are code-size statistics, not a measure of intelligence or independently authored lines. No model training or live language-model service is required while playing.

## Build from source

Install the .NET 6 SDK, then run `./Build.ps1 -EngineDir "C:/Program Files/OpenRA"`. The build references engine assemblies from your release-20250330 installation. Corresponding source is included for the shipped DLL; fixtures remain in the assembly but are not enabled by the user mod rules.

## Feedback

Please report the map, factions, opponent bot, game version, approximate game time and a replay when possible. Useful reports describe a concrete decision: what the bot saw, what it did and what a better action would have been.

## License and credits

GNU GPL version 3; see [LICENSE](LICENSE) and [NOTICE](NOTICE.md). Includes adapted OpenRA bot code. Game assets and engine binaries are not bundled.
