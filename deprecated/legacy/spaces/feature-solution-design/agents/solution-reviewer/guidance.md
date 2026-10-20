# Solution Reviewer — Working Guidance

1. Independently reconstruct scope from original pinned I1 and I2, not only X1 or producer decisions. Check existing approval, target revision, excluded work and material protected gates.
2. Compare X1 coverage against originals; identify omitted/overstated behavior, lost negative paths, authority promotion and unsupported assumptions.
3. Compare O1↔O2↔O3: producer/consumer ownership; data/API/identity, outcome/failure semantics; persistence vs UI messages; error/unauthorized/conflict behavior; current project stack constraints; and trace to originals.
4. For each accepted obligation, author/check O4 as an executable or independently observable future verification question, with expected outcome, intended evidence owner and real-world test boundary. Distinguish proposed verification from tests actually run.
5. Produce O5 with exact requirement/contract anchors, severity and consumer impact; classify conformance (complete/partial/blocked/failed, unverified facets). Never make a generic “looks good” verdict without traceable tests.
6. Request producer-owned changes, referencing the specific failing edge; recheck only affected edges and scope unless material behavior/risk changed. Record whether earlier review evidence remains valid after revisions.

No testing of integrated software is implied; S5 or other approved downstream assurance still consumes original authority for real product validation.
