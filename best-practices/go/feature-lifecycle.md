# Feature Lifecycle: Not-Yet-Active Code

## Disable a feature with a flag, not by commenting out code

**Principle:** Code that can't be activated yet (waiting on an external prerequisite — a downstream registration, an infra dependency not yet ready, a coordinated rollout, etc.) should stay **live** and compiler-checked — not hidden inside a comment.

**Why this happens:** when writing code for a feature that's explicitly "not allowed to go live yet," the easiest reflex is to comment out the call site with a `// TODO`. It looks safe but actually makes the code behind it unreachable and unverified.

### Bad
```go
// TODO: activate once the downstream workflow is registered.
// return ths.buildNotification(ctx, entity, target)
logger.Info(ctx, "action fired: ...")
_ = target
return nil
```
`buildNotification` is unreachable — no test can verify its payload without manually uncommenting it. If the downstream request type changes shape, nothing catches it. `_ = target` is a symptom of this problem: a variable kept alive only to silence the compiler, because the code that would actually use it is dead.

### Good
```go
// TODO: flip to true once the downstream workflow "xyz" is registered.
const notificationEnabled = false // or var — see note on config-driven toggles below

func (ths *service) buildNotification(...) *notificationclient.TriggerRequest {
    // ... target/recipient resolution still runs (exercises this path in staging) ...
    if !notificationEnabled {
        logger.Info(ctx, "notification suppressed, downstream workflow not yet registered")
        return nil
    }
    // construction code below is LIVE — checked by the compiler on every build
    return &notificationclient.TriggerRequest{...}
}
```
Activation is just `false` → `true`, one token, not uncomment + remove logger + remove the placeholder assignment.

**Checklist:**
- If a plan says "not activated until prerequisite X is met" → design it as a flag (`const`/`var`/config toggle), not as commented-out code.
- Code unreachable by the compiler is code no one is testing.
- Prefer keeping the surrounding resolution/setup logic live even while the flag is off — it exercises real code paths (e.g. in staging) instead of leaving them entirely cold until activation day.