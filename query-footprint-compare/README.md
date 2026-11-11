# Query Footprint Compare

A local JetBrains IDE tool for comparing **observed MyBatis Preparing events** across two saved captures of the same scenario. It highlights new SQL templates and growth beyond a chosen per-template budget. It does not measure actual database executions, latency, correctness or N+1 queries.

## Use

1. Capture the same workload before and after a change using existing MyBatis DEBUG logging. No agent or JDBC instrumentation is installed by this plugin. Use fictional/staging data you are allowed to inspect.
2. Save UTF-8 plain text files. Each single-line `==> Preparing:` event must be immediately followed by its single-line `==> Parameters:` line. Interleaved threads and multiline templates are rejected; isolate one request/thread before using the tool. Other lines outside those pairs are ignored.
3. In the IDE choose **Tools → Query Footprint Compare…**. Select two different saved files and an allowed increase for each existing template. New templates fail by default. If you explicitly allow new templates, the growth budget applies only to templates already in the before capture.
4. Compare. Select a row to read the complete template. `REMOVED` is visible but does not fail. `PASS` means only that these captured counts meet the selected policy. Different traffic, logging configuration, caching or batch behavior can change counts independently of performance.
5. Export to a **new** JSON file. Changes to settings invalidate the current result; file hashes and unsaved IDE documents are checked before export. The report is a snapshot, not continuous monitoring.

## Supported format and limits

8 MiB per capture, 100,000 physical lines, 32,768 characters per line, 2,000 distinct templates per capture. Valid UTF-8, optional BOM, LF/CRLF. ANSI escapes, NUL, empty/truncated pairs, symbolic-link inputs, unmatched quotes and PostgreSQL dollar quoting are unsupported. SQL is not parsed or validated: whitespace outside single/double/backtick/bracket quotes is collapsed; case, literals and punctuation remain significant. These rules may split semantically equivalent queries.

Parameters are never reconstructed or exported. Templates can still contain sensitive literal values. Review JSON before sharing. There is no automatic redaction or database access.

## Installation and commercial status

Private evaluation 0.1.0 and a paid candidate 1.0.0 are separate artifacts. The paid candidate uses JetBrains signed-entitlement validation. Its prepared product code is not an assigned Marketplace registration. No actual paid activation or sale is implied. Supported IDE build branch: IntelliJ Platform 252; other versions are not claimed. A private evaluation must not be uploaded as a free Marketplace release.

See [privacy](PRIVACY.md), [license](EULA.md), [validation](VALIDATION.md) and fictional [examples](examples). Support: hello@bizzkitt.ai.

Developed with AI assistance. Automated and native evaluation are agent checks, not human review or customer acceptance. BizzKitt BV is not endorsed by JetBrains or MyBatis.
