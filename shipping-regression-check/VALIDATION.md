# Validation — 10 November 2026

Two isolated WordPress Playground environments actually ran the plugin against real WooCommerce core shipping classes:

| WordPress | WooCommerce | PHP.wasm | Database | Result |
|---|---|---|---|---|
| 7.1.4 | 11.2.2 | 8.3 | SQLite | 38 PHP checks + 3 HTTP checks passed |
| 7.0.8 | 11.1.2 | 7.4 | SQLite | Same 38 PHP checks + 3 HTTP checks passed |

These are **41 unique automated cases across two configurations**, not 82 different tests. Cases include real flat/free/pickup rates, minimum thresholds, changed amounts/formulas, unsupported methods, custom-hook refusal, permission/nonce failures, input boundaries, invalidation and actual HTTP JSON export.

Chrome on macOS additionally showed 3 PASS cases; saving an edited expectation removed the old report and disabled export; running showed 1 FAIL and 2 PASS; the actual browser download contained those results. All data was fictional. No customer acceptance, order or payment is implied.

Native PHP with MySQL/MariaDB, the official Woo QIT suite, broad extension coexistence, other OS/server configurations, full accessibility audit and Marketplace review remain unverified. HPOS compatibility is declared because the plugin does not interact with order storage; this declaration is not a full checkout or migration test. PHP 7.4 coverage is for compatibility only; it is end of life.

Reproduce using the repository's tests/run-integration.mjs and the separately reviewed/pinned local Playground toolchain; the test-only runtime, download archives and fixture database are excluded from distribution. The marketplace engine binds validation receipts to the exact source inventory. Do not reuse results after a source change.
