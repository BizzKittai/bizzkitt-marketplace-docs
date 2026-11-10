# Release Boundary Check

Inspect the actual contents of a ZIP/JAR release against a saved allow, deny and required-file policy inside IntelliJ IDEA. Inspect bounded nested ZIP/JAR archives and export a snapshot report before you distribute a release.

**Status, 10 November 2026:** version 1.0.0 was received by JetBrains Marketplace as plugin 35969 and is hidden, under review. Pricing/licensing setup is currently unavailable. Genuine paid activation, final pricing and public sale remain pending. This repository contains documentation and fictional examples only, not the proprietary plugin or an evaluation download.

## Workflow

Open **Tools → Release Boundary Check**. Select your release archive and JSON policy, choose **Check release**, inspect findings and export JSON to a new filename. Inputs are rehashed before export. Editing an input path invalidates the result. Existing export files are not overwritten.

In the fictional test distribution, the good archive passes with four entries. The bad archive has five entries and four findings: nested `.env`, denied/disallowed test content and missing `LICENSE.txt`. Names are inspected; the plugin never executes archive entries. See [policy format](POLICY.md).

## Meaning and limits

PASS means that the inspected snapshot meets the explicit policy. FAIL means a completed inspection found violations. INCOMPLETE means an integrity, format or resource limit prevented complete inspection and is not PASS. Errors are shown separately.

ZIP/JAR only, including nested entries identified by .zip/.jar extension. No tar/TGZ/7z. Not a secret-content or malware scanner, deployment test, SBOM generator or compliance certificate. Meaningful policies and separate security/deployment checks remain necessary.

Limits: selected archive 50 MiB, individual entry 20 MiB, total expanded bytes 100 MiB, 20,000 entries, two nested levels, 500 displayed findings. Expanded accounting includes nested containers and their contents. Entry paths are never extracted; temporary bounded archive snapshots may be written and cleaned up.

## Tested scope

57 distinct checks: 49 core and 8 invalid-license cases. Official Plugin Verifier 1.411 passed for IntelliJ IDEA Community 2025.2.6.4 / IC252.28539.149. Native macOS ARM64 evaluation verified PASS, four findings, invalidation and actual JSON export. Other IDE versions/OS and genuine Marketplace activation remain unverified. These are internal software tests, not customer endorsements.

## Support and terms

[License terms](EULA.md) · [Privacy](PRIVACY.md). Contact **hello@bizzkitt.ai** with versions and a fictional reproduction. Never send production archives, secrets, payment details or license tokens. BizzKitt BV is the developer; JetBrains operates its separate marketplace services.

A €49 annual license and 14-day trial are proposals only. No checkout or license is supplied by this documentation repository. Final terms and taxes will appear on the authorized store when available.

## Development disclosure

Original BizzKitt implementation with AI assistance, reviewed and tested by the Codex agent. No human code review, buyer, order or earnings are claimed.
