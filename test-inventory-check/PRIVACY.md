# Test Inventory Check — privacy

BizzKitt BV, hello@bizzkitt.ai, 11 November 2026.

The plugin reads the inventory JSON and JUnit XML you choose locally. It writes a new report only on Export. The checker implements no uploads, telemetry, model calls or project/test execution. JetBrains independently handles licensing, updates and purchases under its own terms.

Exported JSON contains test identity names, file basenames, SHA-256 hashes, status/counts/policy and snapshot time. It excludes report stdout, stacktraces, failure-message contents and absolute input paths. Names can still reveal confidential information; review before sharing. Results remain in memory until the dialog closes. Exported files remain where saved until you remove them.

Support uses only material you voluntarily send to handle the request. Send fictional examples, never credentials or real customer reports. Contact hello@bizzkitt.ai about support correspondence.
