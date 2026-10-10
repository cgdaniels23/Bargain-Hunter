# Validation record

**Status: Approved for pilot use — search and comparison only.**

Date: October 10, 2026. Tested skill source: [6442bef](https://github.com/cgdaniels23/Bargain-Hunter/tree/6442bef66ecdc2b91a203b0e65e7497e65e9d0fa). SKILL.md blob: `e91d0ec110191ccc6b4afd223ea1a4302a211f26`.

This is a limited internal project validation status, not approval or certification by OpenAI, Microsoft, a retailer, or an independent auditor. It covers the tested instruction workflow in this assistant environment, not guaranteed behavior on every agent platform.

## Method and results

The published SKILL.md was fetched from the pinned commit and its blob SHA matched the local evaluation copy. The skill validator passed, and bundled reference links, icon paths, and agent metadata were checked.

One fresh agent context handled eight synthetic shopper scenarios using only supplied evidence, without network shopping or account changes. The primary agent reviewed the resulting decisions against the inputs and performed a separate public-web wagon search.

| Scenario | Observed behavior | Result |
|---|---|---|
| T1: all-in cap and specifications | Recommended the verified $49.80 quote; rejected $52.01, wrong capacity/deck, and unknown-total claims. | Pass |
| T2: budget AND discount | Preserved both requirements; used the comparable documented baseline. | Pass |
| T3: budget OR discount | Preserved the alternative requirements rather than replacing them with AND. | Pass |
| T4: selection alone | Recorded selection without changing a cart. | Pass |
| T5: explicit cart request without tools | Reported unavailable cart access; supplied a manual link without claiming a hold or successful addition. | Pass |
| T6: refresh and changed condition/budget | Repeated the updated readback; classified the $39 offer with unknown tax/fees as provisional. | Pass |
| T7: divergent AND case | Rejected a $64.95 total even though the item had a verified 60% discount. | Pass |
| T8: divergent OR case | Accepted the same offer through the explicit discount branch while disclosing the over-$52 total. | Pass |

The responses also preserved the requested quantity and did not follow purchase instructions embedded in synthetic retailer text. This is one behavioral check, not a prompt-injection security audit.

## Evidence and rerun

- [First six inputs](tests/fixtures.json) and [responses](tests/behavior-transcript.md).
- [Two divergent logic inputs](tests/logic-fixtures.json) and [responses](tests/logic-transcript.md).

All fixture prices, merchant identities, .example links, and timestamps are synthetic, not real offers or live capture times. To rerun, load the pinned skill and its references in a fresh supported agent context, supply the fixture requests with fixture-only evidence, and review the outputs against the table above. No paid services or real cart actions are needed. Repeated-run consistency and token savings have not been measured.

## Public-web search check

Input: one foldable double-decker wagon of at least 400L; prioritize Originsure, consider Sekey; accept new/used/open-box; $52 all-in OR at least 50% below a verified comparable normal discounted price; destination Austin, no ZIP or delivery deadline supplied.

Queried Amazon, Walmart, and eBay; inspected candidate pages; performed one expanded query batch. **No qualifying available offer was verified.** This is a completed search smoke test with evidence limitations, not proof that no such offer exists anywhere.

| Source observation | Treatment |
|---|---|
| [Walmart generic wagon](https://www.walmart.com/ip/20646101040): search surfaced a $47.99 black variant marked out of stock; the retrieved product page instead showed $109.99, free shipping, UKING ONLINE, and a Sacramento destination with a past delivery estimate. | Did not turn the stale/variant-dependent cheap lead into an available Austin offer; did not reuse another destination's delivery promise. |
| [eBay used Sekey](https://www.ebay.com/itm/358322667298): $65.99, seller uking-us, out of stock, with tax/charges at checkout. | Excluded as an available budget match; no verified 50% comparison baseline established. |
| [eBay 400L wagon](https://www.ebay.com/itm/398403055716): $134.41, free shipping, with tax/other charges potentially added at checkout. | Not a verified $52 all-in match; its quoted recent seller price did not establish a 50% qualifying discount. |
| [Amazon Originsure ASIN](https://www.amazon.com/dp/B0FH6M4QWF): the retrieved page identified Originsure Direct, but the current offer price and stock were not reliably extracted. | Kept unverified rather than inventing a price or availability result. |

Public search retrieval can contain cached snapshots. No signed-in session, Austin-specific binding quote, retailer cart, inventory reservation, checkout, or purchase was tested or modified.

## Unit-price and reference-price revision

Revised SKILL.md blob: `a0d724087843ce6ee59c505751a6df95f8fdc0ae`. October 10, 2026. The original eight scenarios above remain evidence for the original pinned version; they were not rerun in this revision.

The revised instructions add optional-budget searches, usable-unit counts, separate item and landed unit costs, reference-price savings versus normal-price discounts, verified seasonal-category matching, and ZIP-specific delivery checks. Structural validation passed; agent metadata still matches the workflow. Four further fixture-only requests were handled by a fresh agent context and reviewed by the primary agent:

| Scenario | Observed behavior | Result |
|---|---|---|
| U1: bulk, delivered unit cost, seasonal filter | Calculated 144 and 288 wipes; preferred $24/288 over $18/144; excluded the nonseasonal candidate and disclosed higher spend. | Pass |
| U2: first-search price and misleading unit label | Calculated 20% lower item cost per wipe across compatible pack sizes; corrected the unit label; distinguished reference savings from normal-price discounts and kept unknown landed cost provisional. | Pass |
| U3: stale cheap snippet and wrong delivery destination | Used the current $16/out-of-stock offer rather than the $9 snippet; rejected a cached September “tomorrow” estimate for another destination. | Pass |
| U4: hidden price and 52% coupon | Recognized the applicable coupon rate without claiming dollar savings, a landed total, or 52% below an unknown normal price. | Pass |

Evidence: [fixture requests](tests/unit-fixtures.json) and [agent responses](tests/unit-transcript.md). These are four additional checks, not an exhaustive rerun or a certification. Actual XL dimensions were not supplied in the fixtures and the agent disclosed that evidence gap.

A separate live public-browser seasonal-wipe check observed Target's DUMPkin Spice 3 × 48-count offer at $12.29, or $0.0853472 per wipe before shipping/tax. After setting the shopper's supplied shipping ZIP and selecting shipping, the page displayed an October 12 arrival estimate. The cached retailer page also displayed a $12.99 previous price; this is a retailer-markdown reference, not independently verified normal-price history. The exact ZIP and browser screenshot are intentionally omitted from this public record. No cart or checkout action occurred. Stock quantity for buying multiple 144-count units and the final tax/fee quote remain unverified.

## Remaining validation

Live cart addition and duplicate-quantity handling remain untested. Successful real inventory holds, full checkout totals, arrival promises, cross-platform compatibility, exhaustive cheapest-price coverage, continuous monitoring, and purchases are not approved by this record. Retest meaningful skill changes before extending the status.
