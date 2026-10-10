# Bargain Hunter

**Set your criteria. Compare the offers. Decide what to buy.**

An Agent Skill by Grant Daniels that finds available shopping deals, checks them against your requirements, and returns up to three useful offers with source links.

## The flow

**Humanize Me → read back your criteria → research → compare → choose**

Every request and refresh begins with the bundled [Humanize Me shopping-intent mode](references/humanize-me-shopping.md). It preserves your intent and reads back the product, budget, discount target, condition, shipping, delivery, and seller requirements before research.

The workflow checks up to three relevant retailers initially and expands once if needed. It separates verified matches from offers with unknown costs or missing evidence.

## Use it

Use an agent platform that supports Agent Skills and provides web search or permitted retailer access. Copy `SKILL.md`, `references/`, `agents/`, and `assets/` into a skill folder named `bargain-hunter` using your platform's supported installation method. No separate Humanize Me installation is required for the compact shopping mode.

Example:

> Use $bargain-hunter to find one foldable, double-decker wagon with at least 400 liters of capacity for $52 or less including tax, shipping, and fees. Include new, used, and open-box options.

Provide a destination ZIP/postal code if needed for shipping or tax estimates. Unspecified requirements remain unspecified.

## Optional cart step

After choosing an exact offer, explicitly ask to add it to your cart. This requires available authorized retailer or browser tools; the skill itself does not provide cart access. It verifies the outcome and stops before checkout. Adding to cart does not establish an inventory hold.

## Cost and compatibility

No paid API, hosting, or backend is required by this version. Your assistant's plan limits and any separately enabled tools still apply. The skill is an instruction package, not a standalone shopping service, browser, or always-running monitor. Token costs vary; the workflow limits unnecessary searches and overlapping skill loads.

## Status

**Approved for pilot use — search and comparison only.** Eight synthetic scenarios passed, and a public-web search smoke test completed. Read the [validation record and test evidence](VALIDATION.md) for the exact scope.

Live retailer/cart compatibility remains untested. This is limited internal validation, not third-party certification. Prices and stock can change; unknown tax, shipping, or fees stay clearly marked. No automatic purchases or background monitoring.

## License and credit

[MIT License](LICENSE). Includes an adaptation of [Humanize Me](https://github.com/cgdaniels23/Humanize-Me), created by Grant Daniels, with its [original copyright and license](references/humanize-me-LICENSE.txt) preserved.
