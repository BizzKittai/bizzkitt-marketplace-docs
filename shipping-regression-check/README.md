# Shipping Regression Check

Repeat your shipping expectations after a change. An original BizzKitt BV staging tool for developers and agencies using WooCommerce's built-in shipping methods.

## A concrete example

A fictional T-shirt costs €25. A Netherlands zone has Flat Rate €4.95, Free Shipping from €50 and zone Local Pickup €0. Save cases for quantities 1, 2 and 3. The first should contain flat rate and pickup; the next two also contain free shipping. If you change flat rate to €6.95, the saved expectation of €4.95 fails. The tool shows expected and actual rates and exports the captured result.

The example prices and identifiers are fixtures, not a customer's store, order or commercial result.

## Install and prepare

1. Use a dedicated staging copy with a backup. Set `WP_ENVIRONMENT_TYPE` to `staging`, `local` or `development` using WordPress configuration. Production runs are refused.
2. Activate WooCommerce and this plugin. In this isolated fixture store disable tax calculation and select a currency with two decimals. These are deliberately narrow test conditions, not advice to alter the tax treatment of a real shop.
3. Add a physical **simple** fixture product with SKU `fixture-tee` and a price of 25. Create the zone and three methods above. Do not add orders or real customer records.
4. Find each method's `instance_id` in its WooCommerce shipping-settings URL. Replace the illustrative `flat_rate:1`, `free_shipping:2`, `local_pickup:3` keys in `suite.json` with your own instance IDs. Never assume newly created IDs are always 1/2/3.
5. Open **WooCommerce → Shipping regression**, paste the JSON and **Save suite**. **Run saved suite** always uses the saved version. Saving replaces the old suite and clears its report.
6. Check every result. **Export current report** downloads the suite and report as JSON. Keep separate snapshots yourself if you need history. Version 1 stores only the latest report.

## Scope and meaning

Each case has one SKU, quantity 1–100, a country/state/postcode and exact expected core method IDs and decimal-string amounts. Up to 25 cases and 64 KiB input; up to 10 expected rates per case. No names, addresses or email fields are accepted. A country with required states needs a valid state code.

- **PASS:** the completed core-method calculation returned exactly the saved map of rates.
- **FAIL:** it completed, but returned a different map.
- **UNSUPPORTED:** a missing/non-simple/virtual fixture, unknown shipping method or coupon-dependent Free Shipping prevents this case from being evaluated. No success is implied.
- **ERROR:** a supported calculation raised an error. Review the local WooCommerce logs.

Supported: core Flat Rate including its WooCommerce cost formula, Free Shipping with no condition or a minimum amount, and **zone** Local Pickup. Rates are enumerated from these methods using a synthetic package/cart context. A storefront may apply additional availability, hiding, checkout or customer rules. This is not a simulation of the entire WooCommerce shipping pipeline.

Not supported: tax, coupons, variable products, mixed carts, multiple packages, live carrier quotes, third-party shipping hooks, Checkout-block Local Pickup or end-to-end checkout. Do not run this against a production store. Additional plugins remain executable PHP; the network guard is not a sandbox for them.

## Stale results

The report is tied to saved cases, shipping tables/settings, relevant product properties, shipping classes, source and platform/plugin versions. A relevant change makes export unavailable until the suite runs again. The check does not hash every file of every third-party plugin or prove arbitrary hooks are unchanged. Re-run after any deployment even if its version number was not changed. A report is a point-in-time result.

## Data, license and support

See [privacy](PRIVACY.md), [license and support](TERMS.md) and [validation evidence](VALIDATION.md). Source is GPL-2.0-or-later. BizzKitt's intended commercial offering is supported distribution and updates; no proprietary activation gate is included.

Support: **hello@bizzkitt.ai**. Send versions and a minimal fictional example only. Response targets: two business days for critical reports, five for other reports; no guaranteed resolution time. No purchase is currently available through this candidate.

To remove saved plugin data use **Delete saved data**. Deactivating retains it; uninstalling deletes only the two plugin options. Export any reports you need before removal.
