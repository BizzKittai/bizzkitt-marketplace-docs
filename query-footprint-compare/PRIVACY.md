# Query Footprint Compare — privacy

11 November 2026. BizzKitt BV, hello@bizzkitt.ai.

The plugin reads only the two capture files you choose and writes a new JSON report only when you choose Export. Processing is local. No database connection, JVM instrumentation, telemetry, external model, network request, SQL execution or upload is implemented. JetBrains separately handles Marketplace licensing, updates and purchases under its terms.

The report contains selected basenames, complete-file SHA-256 hashes, normalized SQL templates, observed counts and comparison settings. Parameters lines are not retained or included, but SQL templates and filenames may themselves contain personal data, secrets or literal values. This is not a redaction tool. Review a report before sharing. Files are not copied to a product cloud. Results stay in memory until the dialog closes; exported reports remain where you saved them. Delete your own reports normally when no longer needed.

Support: send only a minimal fictional example, IDE build and plugin version. Do not send production captures, access tokens, customer data or license secrets. Any support correspondence you voluntarily send is used to handle that request; contact hello@bizzkitt.ai about it.
