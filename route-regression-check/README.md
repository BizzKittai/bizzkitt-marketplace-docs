# Route Regression Check

Save the routes that matter in your Unity level, then check reachability, path length and detours after navigation changes.

**Availability, 11 November 2026:** version 1.0.0 is locally built and natively tested. Publisher registration and Asset Store submission are not complete; it is not publicly for sale. These are free product instructions, not a download of the paid extension.

## What it does

- Stores named start/goal positions, an agent type, area mask and expected outcome in a suite asset.
- Checks complete or unreachable routes, with optional maximum length and detour bounds.
- Separates invalid inputs from actual route failures.
- Frames and draws the selected route in Scene view.
- Invalidates results after changes and rechecks before local JSON export.

## Documentation

- [Quick start and limitations](QUICKSTART.md)
- [Tested compatibility](COMPATIBILITY.md)
- [Privacy and report contents](PRIVACY.md)
- [Asset Store license notice](LICENSE-NOTICE.txt)
- [Real report from the fictional included demo](example-report.json)

This release queries static NavMesh data in one saved open scene outside Play Mode. It does not bake navigation, run characters, test collisions or prove gameplay traversal. Projection can select the wrong floor on overlapping NavMeshes. Read the documented limits before use.

Verified with Unity 6000.3.28f1 on macOS ARM64: 44 distinct native Edit Mode cases, visible Editor workflow and a clean import into a separate blank project. The optional demo uses URP 17.3.0. Other operating systems and versions are not claimed as tested.

Support: **hello@bizzkitt.ai**, BizzKitt BV, Netherlands. Send the Unity version, expected/observed result and a minimal fictional reproduction. Never send credentials or an entire confidential project. No response-time guarantee is advertised.

OpenAI Codex assisted source, test, documentation and demo authoring. Review and validation described here were performed by the Codex agent. No human code review, customer endorsement or Unity approval is claimed. Unity is a trademark of Unity Technologies; no endorsement is implied.
