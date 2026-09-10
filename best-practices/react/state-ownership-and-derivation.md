# state-ownership-and-derivation.md

Location: `react/state-ownership-and-derivation.md`

Principle Before introducing state, determine whether the value needs independent ownership at all. A value that is a deterministic projection of existing state should be derived, not stored and synchronized as another source of truth.

When independent ownership is required, place state according to its authority, lifetime, and sharing semantics, using the narrowest owner that satisfies those requirements. Server-authoritative data stays with the data-fetching owner already responsible for it — server render/loader, query cache, or equivalent — rather than being copied into client state for convenience. Navigation state that should be shareable, bookmarkable, or participate in back/forward navigation should generally be URL-owned when appropriate and non-sensitive. Form-lifecycle values belong with the form; ephemeral interaction belongs locally. Shared client state is appropriate only when genuinely client-owned state must span or outlive its natural component boundary.

Bad

```
function RecordPage({ id }) {
  const { data: record } = useRecord(id);
  const setRecord = useRecordStore((state) => state.setRecord);
  const [isActionable, setIsActionable] = useState(false);

  useEffect(() => {
    if (record) setRecord(record); // duplicates server-owned data
  }, [record, setRecord]);

  useEffect(() => {
    setIsActionable(
      Boolean(record?.status === 'ACTIVE' && record.remaining > 0)
    );
  }, [record]); // deterministic projection stored as another state
}
```

Good

```
function RecordPage({ id }) {
  const { data: record } = useRecord(id);

  // record remains owned by its data-fetching layer;
  // isActionable has no independent owner
  const isActionable =
    record?.status === 'ACTIVE' && record.remaining > 0;

  ...
}
```

Ownership decision order

1. Can the value be derived reliably from state that already exists? If yes, derive it instead of introducing another owner.
2. Is an external or server data source authoritative? Keep the value with the existing data-fetching owner rather than mirroring it into client state.
3. Should navigation state be shareable, bookmarkable, or participate in back/forward navigation? Consider URL ownership when appropriate and non-sensitive.
4. Does the value exist for the lifecycle of a form? Keep it with the form.
5. Is it ephemeral interaction state whose consumers share a natural component owner? Keep it local or lift it only to that owner.
6. Use shared client state only when the value is genuinely client-owned and its required lifetime or consumers exceed a natural local boundary.

Checklist

* [ ] No deterministic value is stored solely so an effect can synchronize it with another value
* [ ] Server/external authoritative data is not mirrored into global client state merely for convenient access
* [ ] Share/bookmark/back-forward semantics are considered before navigation-relevant state is kept only in memory
* [ ] Sensitive state is not moved into the URL merely for persistence or convenience
* [ ] Form-lifecycle state stays with the form unless another lifetime is explicitly required
* [ ] Ephemeral UI state starts at the narrowest meaningful owner rather than defaulting to context/global state
* [ ] Shared client state has a concrete lifetime or cross-tree requirement that local ownership cannot satisfy
