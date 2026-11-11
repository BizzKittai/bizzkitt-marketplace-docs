# Route Regression Check

Version 1.0.0 — BizzKitt BV

Keep an explicit record of the routes that matter in a level, then check them after level edits or a navigation rebake. This is an Editor tool for static Unity NavMesh queries. It does not run a character, simulate physics or repair navigation.

## First check

1. Import the package into a backed-up project. Open one scene with navigation baked for your intended agent type. Save the scene. The tool never bakes or opens your scenes automatically.
2. Open **Tools > BizzKitt > Route Regression Check** and choose **New suite**. Save the asset in your project. It is bound to the currently open saved scene.
3. Choose **Edit suite**. Expand Routes in the Inspector and edit the first route. Give it a unique descriptive name, start and goal world positions, and the configured agent type ID.
4. Keep the projection radius small. The default is 0.5 world units. Pick an area mask that matches your character's navigation permissions. `-1` includes all areas; an empty mask is invalid.
5. Choose **Complete** when the route must exist. Optionally set maximum path length and maximum detour ratio. Zero turns a bound off. Choose **Unreachable** when both endpoints should remain on navigation but should not be connected; leave the two length bounds at zero.
6. Select **Run route checks**. Click a result to frame its route in Scene view. **Export JSON** saves a local report; it does not upload anything.

To capture positions from scene objects, select two objects with the intended goal as the active selection, then choose **Add selected pair**. This copies their current world positions. The route is not attached to the objects and will not follow later movement. Review the positions in the Inspector.

## Included example

Open `Examples/RouteDemo.unity` in a URP project. Its demonstration-only component loads the included baked NavMesh. Select `PassingRoutes.asset`, then run the checks. `FailingLengthBound.asset` intentionally sets the first route's maximum length too low, demonstrating a regression finding. The geometry and NavMesh are the same for both suites; the second suite is an intentionally failing test, not a simulation of a performed customer level edit.

The demo navigation component is optional and is not required for your scenes. Use your own normal NavMesh workflow. Remove the Examples folder if it is not needed in your project.

## Understanding results

- **PASS**: the observed route satisfies its configured expectation and bounds.
- **FAIL**: the query ran with valid projected endpoints, but its outcome violates an expectation.
- **ERROR**: the case cannot be evaluated reliably, for example because an endpoint is off-mesh, an agent type is absent, a mask is empty, or a value is invalid. An error never counts as a successful unreachable route.

`CalculatePath` can return true for a partial path. This tool also checks its path status. Both endpoints are projected using the same explicit agent type and area mask. Reports include the requested and projected positions, projection distances, corners, actual path status, query result, length and configured bounds.

## After a change

Save the scene, rebake using your normal workflow if geometry or navigation settings changed, then run checks again. Existing results are marked stale after scene, asset or suite edits. Export checks the current input fingerprint and re-queries all routes to catch navigation changes that are not represented by mesh geometry. If either changes, export is refused until you run again. Export does not silently replace the results you reviewed.

The checker cannot determine whether a bake matches your current scene geometry. A saved scene can still have an old bake. Save and rebake deliberately before drawing conclusions.

## Limits and interpretation

- One saved scene at a time, outside Play Mode. Additive scenes, dynamic runtime carving, custom navigation engines and agent-local area-cost overrides are outside this release's scope.
- Routes use the project's global area costs. Length is the sum of corner-to-corner distances in world units, not travel time, weighted cost, collision clearance or proof of the shortest geometric route.
- Projection does not consider walls or ceilings. In overlapping or multi-floor navigation, the nearest surface may be the wrong floor. Use small radii, review projected positions, and avoid overlapping NavMeshes of the same agent type in a test scene.
- A complete NavMesh path does not prove that a moving character can traverse it. Movement controllers, animations, links, avoidance and physics require separate gameplay tests.
- Synchronous navigation queries may take time on large levels. This release bounds a suite at 200 cases and its fingerprint inspection at 250,000 vertices / 1,500,000 indices to limit Editor work and memory. There is no paid unlock or hidden subscription. Split large regression suites into focused scenes/suites.
- The initial compatibility target is Unity 6000.3 LTS. See [Compatibility](COMPATIBILITY.md) for versions actually tested; a target is not a compatibility claim.

## Support

Contact `hello@bizzkitt.ai` with your Unity version, a minimal synthetic reproduction and the expected result. Review reports before sharing them: they contain your scene and suite paths within the project, route names and positions. Do not send credentials, customer data or an entire confidential project. No response-time guarantee is promised.
