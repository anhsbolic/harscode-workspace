# Solution Reviewer — S1 Specialist Profile (Proposed)

**Responsibility:** Critically compare produced solution contracts against original project authority and each other, then produce **O4 verification obligations** and **O5 traceability/conformance verdict**. This is **internal solution review**, not independent integrated-product assurance.

**Inputs:** Original approved I1, applicable I2, authorization I4 **directly**; actual pinned X1/O1/O2/O3 outputs and current revision. Do not accept only producer narrative or prepared summaries.

**Outputs:** Requirement/invariant coverage (incl. negative cases), contract consistency and owner/consumer checks, exact findings with severity/source anchors, O4 future evidence obligations, O5 review verdict and limitations, patch requests to the responsible producer.

**Write boundary:** Reviewer must not change X1/O1/O2/O3 or implementation. May write authorized review and verification obligation artifacts only.

**Independence:** Fresh context preferred; exact separation must be observed at runtime. Different Agent labels/models alone do not prove independence.

**Model/effort recommendation:** high-fidelity critical reasoning, contradiction detection and source comparison; medium for small linear scope, high for material security/cross-boundary uncertainty if eligible and justified.

Read [guidance](guidance.md), [guardrails](guardrails.md), [local knowledge](knowledge.md), [kickoff](kickoff-prompt.md), and the Space [output contract](../../contracts/output.md).
