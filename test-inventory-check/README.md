# Test Inventory Check

A local IntelliJ IDEA tool for checking an explicit required test inventory against one saved JUnit XML report. A nonempty green report can omit tests: this tool reports required identities absent from that report. It does not execute tests, discover them from source, authenticate a report, establish current CI state or diagnose the reason a test was omitted. It is not coverage measurement.

## Use

Install the private evaluation ZIP from disk in a dedicated test IDE, restart if prompted, and choose Tools → Test Inventory Check. Do not publish the evaluation as a free marketplace version. The separate paid candidate requires an authentic Marketplace entitlement; a proposed code is not an entitlement.

Choose a saved inventory JSON and a saved report XML. The inventory is an explicit requirement you review and maintain; this tool intentionally does not generate or approve a baseline from the report being checked.

```json
{"schema":1,"required":[{"class":"demo.CheckoutTest","name":"freeShippingThreshold"},{"class":"demo.CheckoutTest","name":"pickupAvailable"}]}
```

Class and name compare exactly, including parameter display names and whitespace. A required identity must occur exactly once and have no failure, error, skip or retry/flaky outcome. Missing/failed/error/skipped/flaky required cases fail. Extra identities are listed; they fail only when “Fail on unexpected test identities” is selected. In permissive mode an extra failed test does not fail this required-inventory check; the original report remains the source for overall test-run failures.

## Supported format and limits

One UTF-8 JSON file up to 1 MiB; schema 1 with only `schema` and `required`; each entry has only string `class` and `name`. Up to 10,000 identities, 512 characters per identity component; no controls, blank values or duplicates.

One UTF-8 XML file up to 8 MiB; top-level `testsuite`, or `testsuites` containing flat `testsuite` children. Every `testcase` needs `classname` and `name`. Optional aggregate tests/failures/errors/skipped counts must match testcase elements. Standard failure/error/skipped text and flat flakyFailure/flakyError/rerunFailure/rerunError outcomes are recognized. `properties`, `system-out` and `system-err` metadata may be present. Nested suites, namespaces, nested result/output markup, unknown extensions and conflicting outcomes are rejected. Duplicate class/name identities across suites are ambiguous, not silently merged. This deliberately bounded subset is not a universal JUnit XML validator.

DOCTYPE, external entities/resources and leaf symlink inputs are refused. No project code, network call or external model is invoked by the checker. Large/unsupported/invalid input yields INCOMPLETE, never PASS. An empty XML suite is valid but fails all required identities.

## Reports and stale results

Review the table and selected identity detail. Setup changes invalidate results. Save edits to inputs before checking/exporting. Export writes a new JSON file only; it does not overwrite an existing file. Both input hashes are checked at export. A snapshot can be stale relative to CI even if the local bytes remain unchanged.

Exports include identity names, input basenames, content hashes, counts, policy and outcome. They omit stdout, stack traces, failure messages and absolute input paths. Names/filenames may still be confidential: review before sharing. No file is uploaded by the plugin.

## Fictional demonstration

`examples/required.json` + `examples/pass.xml`: PASS.
`examples/required.json` + `examples/missing.xml`: FAIL because pickupAvailable is absent, although the XML reports one passing test.
`examples/required.json` + `examples/skipped.xml`: FAIL/SKIPPED.
`examples/ambiguous.xml`: INCOMPLETE due to duplicate identity.

Only actual dated validation receipts establish executed tests, native behavior or compatibility. Intended runtime: IntelliJ IDEA CE 2025.2 branch, JDK21, macOS ARM64. Other IDE versions/OS and customer projects are not claimed. No real paid/trial activation or marketplace approval is implied by local test execution.

Support: hello@bizzkitt.ai. Send only a minimal fictional report/inventory and the plugin/IDE version. Do not send customer data, credentials or license tokens. Original BizzKitt BV implementation with AI assistance; owned platform/license infrastructure reused, original parser/workflow/tests. No customer testimonials, paid demand or sales are asserted.

See [license](EULA.md), [privacy](PRIVACY.md) and [validation](VALIDATION.md). Status: tested local candidate; no public sale or provider approval.

## Version 1.0.1 (12 November 2026)

Version 1.0.1 installs in IntelliJ-based IDEs from 2025.2 onwards; version 1.0.0 was limited to branch 252. It has
no functional changes. The 68 automated checks passed again, and the JetBrains Plugin Verifier 1.411 reported
Compatible against IntelliJ IDEA 2025.2.6.4, 2025.3.6.2, 2026.1.5.1, 2026.2.4 and 2026.3. The newer IDE versions
were not tested by hand.
