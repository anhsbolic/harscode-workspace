# Rendered Experience Assessment and Correction Feedback

> **Applicable when:** actual implementation exists and Craft feedback must be grounded in source or rendered behavior. Framework lint/build/unit test success does not prove spatial correctness.

## Evidence selection

Review only representative surfaces/states/viewports that could reasonably disprove the implementation: initial page; consequential form/confirmation; validation/error/unknown or long-content state; narrow and wide layouts if composition changes; overlay and keyboard/focus if present. Do not multiply scenarios into an exhaustive grid. Project SOP controls whether assessment is performed through interactive browser, manual Human QA, screenshots or permitted automation.

An image or screenshot can support visual observations but does not by itself prove keyboard behavior, request handling, responsive reflow at other sizes or complete navigation. Source-only review should be labeled **source inspection**. If rendered access is unavailable or SOP assigns it externally, report NOT VERIFIED or manual-owner handoff instead of inventing a PASS.

## Actionable findings

For each material issue, give: exact implementation revision; URL/surface/state/viewport or source anchor; observed failure; applicable authority or usability risk; effect on user; recommended correction; whether it blocks scope. Example: “At narrow width the pre-submit consequence text is omitted, changing the informed action” is testable. “Feels too generic” without purpose, authority or evidence is not.

Engineer owns corrections. Re-examine affected states after a change if permitted; a prior screenshot/review conclusion may no longer match the corrected revision. Do not certify your own production implementation as independent assurance, and do not claim to have reviewed assets or tool output you never saw.
