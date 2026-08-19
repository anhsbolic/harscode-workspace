# go/examples.md

> Real-world references for files in `go/`. Kept separate from the principle
> files themselves so those stay project-agnostic — this file is where the
> concrete, implementation-level detail lives instead.
>
> Entries added only via `proposals/` review (see `proposals/README.md`) —
> not agent-appendable directly, unlike `techplan/examples.md`.

---

## For: `jwt-and-token-lifecycle.md`

**Context:** an account domain with a standard login flow plus an MFA
step-up flow (login succeeds → MFA required → separate verification step
before a full session is issued).

**What was done:** two structurally different token types were issued for
two different trust levels in the same flow:

- **Access token** — signed with **ES256** (asymmetric). Represents a
  fully authenticated session with full scope.
- **`mfa_pending_token`** — signed with **HS256** (symmetric), a
  completely separate key from the access token's. Represents an
  intermediate state: password verified, MFA not yet completed. Narrow
  scope — valid only for the MFA-verification endpoint, nothing else.

**Why it matters:** the two tokens were kept on fully separate signing
material on purpose, not just a different `scope` claim under the same
key. Reasoning: if the MFA-pending issuance path is ever looser than
intended (e.g. a bug lets it get generated too easily, or with a longer
expiry than meant), that weakness stays contained to the narrow-scope
token. It cannot be leveraged to forge or tamper with a full access token,
because the two don't share a key or algorithm family at all. A shared
key would mean a weakness in the low-trust issuance path directly
threatens the high-trust one.

**Generalizable takeaway:** when a system has more than one token
"trust level" in the same auth flow (pending-verification vs. fully
authenticated is the most common shape, but this generalizes to any
step-up flow), don't treat it as "same token type, different claim."
Treat it as different token types with independent signing material,
so a compromise of the narrower one is structurally incapable of
escalating to the broader one.