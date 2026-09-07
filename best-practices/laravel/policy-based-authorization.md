# policy-based-authorization.md

**Location:** `laravel/policy-based-authorization.md`

**Principle**
A middleware permission gate (`can:edit-invoice`) answers "is this actor allowed to do this *kind* of action" — it says nothing about *which specific resource*. A query scope (`whereHas('tenant', ...)`) answers it correctly only if every query path to that resource remembers to apply the scope, which is exactly the kind of thing a newly added endpoint, an admin override route, or a report/export path is likely to forget. Neither mechanism is a resource-level ownership check on its own. An explicit, independent check inside a Policy or `FormRequest::authorize()` — verifying the requested resource actually belongs to the requesting actor/tenant/scope — is a second layer that has to be actively bypassed rather than accidentally omitted, because it lives with the resource-fetching logic itself, not with routing or query construction.

**Bad**
```php
// routes/invoices.php
Route::get('/invoices/{invoice}', [InvoiceController::class, 'show'])
    ->middleware('can:view-invoices'); // gates the ACTION, not the resource

class InvoiceController extends Controller
{
    public function show(string $invoiceId)
    {
        // No ownership check — any authenticated user with the general
        // "view-invoices" permission can fetch ANY invoice by guessing/incrementing IDs.
        $invoice = Invoice::findOrFail($invoiceId);

        return response()->json($invoice);
    }
}
```

**Good**
```php
class InvoicePolicy
{
    public function view(User $user, Invoice $invoice): bool
    {
        // Explicit, independent resource-scope check — separate from any
        // middleware permission gate, and re-verified on every access.
        return $invoice->tenant_id === $user->tenant_id;
    }
}

class InvoiceController extends Controller
{
    public function show(Request $request, Invoice $invoice)
    {
        $this->authorize('view', $invoice); // throws 403 if the Policy check fails

        return response()->json($invoice);
    }
}

// Negative-path test — not just "user without permission gets 403"
class InvoicePolicyTest extends TestCase
{
    use RefreshDatabase;

    public function test_user_cannot_view_invoice_from_another_tenant(): void
    {
        $tenantA = Tenant::factory()->create();
        $tenantB = Tenant::factory()->create();
        $user = User::factory()->for($tenantA)->create();
        $invoice = Invoice::factory()->for($tenantB)->create();

        $this->actingAs($user)
            ->getJson("/invoices/{$invoice->id}")
            ->assertForbidden(); // has the "view-invoices" permission, still blocked
    }
}
```

**Checklist**
- [ ] Every endpoint that returns or mutates a specific resource by ID has an explicit ownership/scope check in a Policy or `FormRequest::authorize()` — not only a middleware permission gate
- [ ] A negative-path test exists for cross-tenant/cross-owner access (an actor *with* the general permission, requesting *someone else's* resource) — not just a "no permission at all" test
- [ ] Query scoping (`whereHas`, tenant scope) is treated as defense-in-depth/optimization, never the sole authorization mechanism
- [ ] A newly added endpoint on an existing resource is checked in review for whether it inherited the same Policy check, rather than assumed correct by precedent
- [ ] Admin/override routes and export/report endpoints are held to the same resource-level check as the primary CRUD routes for that resource, not exempted by convention
