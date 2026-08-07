# Abstraction Boundaries & Responsibility

## 1. The function name is the contract. The return type must not leak other responsibilities

**Principle:** If a function's name promises one thing ("update status"), its return type and body must not silently add other responsibilities (a network call to a third-party service, building a downstream payload, etc). SRP applies down to the signature level, not just the body.

**Why this happens:** when asked to "add feature X to flow Y," the fastest path is to bolt the new logic directly onto the existing function for Y — rather than emitting a new observation/value and lifting the decision about X to the caller.

### Bad
```go
func (ths *service) updateStatus(...) (*downstreamclient.TriggerRequest, error)
```
This function now changes when: (a) status-transition logic changes, (b) the downstream request format changes, (c) recipient/target resolution changes, or (d) the payload shape changes. Multiple independent reasons to change = an SRP violation baked into the signature.

### Good
```go
func (ths *service) updateStatus(...) ([]string, error)
```
The function only knows "what changed and is relevant to my domain." The decision of "is this enough to trigger the downstream action" and the payload construction move to the caller, which already has the full context to make that call.

**Checklist:**
- Before adding a new parameter/return value to an existing function, ask: "is this addition part of the responsibility the function's name promises?" If not, that's a signal to lift the logic to the caller instead of piling it onto this function.

---

## 2. Separate pure predicates from side-effecting actions

**Principle:** Decision-making logic (boolean/pure logic) should be extracted as much as possible into a pure function with no receiver and no external dependency (network, DB, tracer). Genuinely side-effecting actions (network calls, logging, tracing) belong in a separate layer.

**Why this happens:** merging "check the condition" + "execute the action" into one method is natural when writing code top-down following the narrative flow — but it tanks testability and inflates test count without adding real coverage.

### Bad
```go
func (ths *service) detectAndBuildNotification(
    ctx context.Context, old, new *Entity, changedFields []string,
) *notificationclient.TriggerRequest
```
The name "detect **and** build" signals two responsibilities in one compound verb. To test the detection condition alone, you need a fully-stubbed `*service` (tracer, feature toggle, downstream client) even though the condition itself is pure logic.

### Good
```go
// pure function — testable with zero mocks
func shouldTriggerNotification(old *Entity, changedFields []string) bool

// method with side effects — tested separately, fewer mocks needed
func (ths *service) buildNotification(
    ctx context.Context, entity *Entity, fields []string,
) *notificationclient.TriggerRequest
```
The predicate becomes a plain `require.Equal(t, want, shouldTriggerNotification(entity, fields))` — no setup, no teardown, no mocks.

**Checklist:**
- If a function name contains a conjunction ("and", "detectAnd...", "checkAndDo...") → suspect two responsibilities that can be split.
- A pure predicate should not have a struct receiver unless it genuinely needs internal state (not just for convenience of colocating code).

---

## 3. Don't extract a new layer just to make one caller easier to test

**Principle (YAGNI for indirection):** New functions/abstractions should only be created when there's a real need (multiple callers, or a clearly distinct lifecycle). A function with a single caller that exists solely to avoid testing through that caller is a daily maintenance cost for a benefit that may never materialize.

### Bad
Two functions: `detectAndBuild` (detection + context lookup + logging, which calls) → `construct` (builds the final payload). Reason for splitting: so the constructor could be tested without stubbing the context-lookup dependency.

### Good
Once the predicate is extracted as a pure function (see item 2 above), the constructor's only remaining caller is the builder itself. Fold it into one function. The "test without the dependency" concern is solved with a feature flag (see `feature-lifecycle.md`) + a stub for the dependency returning a canned response — not by splitting into layers whose only purpose is test isolation.

**Checklist:**
- Before proposing a new function/interface split, ask: "who are the callers now, and who might they be later?" If the answer is "one, and only for testing," consider another mechanism (flag, simple dependency injection) first.