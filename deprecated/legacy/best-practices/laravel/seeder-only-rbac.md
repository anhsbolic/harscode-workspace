# seeder-only-rbac.md

**Location:** `laravel/seeder-only-rbac.md`

**Principle**
Every runtime create/update/delete endpoint for roles and permissions is a target — it's code that has to be authorized correctly, audited, and kept safe from privilege-escalation bugs, for a capability (changing who can do what) that most apps only actually need to configure a handful of times, usually at deploy time. If the app's roles are a small, stable set defined by the business (not something end-users create per-tenant), restricting all role/permission mutation to seeder classes — run as part of deploy, never exposed as an endpoint — removes that entire class of runtime attack surface instead of just gating it more carefully. The trade-off is real: this doesn't fit an app that needs tenants to define their own custom roles, because there's no runtime mechanism left to do that.

**Bad**
```php
// A runtime RBAC management endpoint — even correctly permission-gated,
// this is now a standing target: a privilege-escalation bug here grants
// arbitrary permissions, and it exists for a capability rarely used after launch.
Route::middleware('can:manage-roles')->group(function () {
    Route::post('/roles', [RoleController::class, 'store']);
    Route::put('/roles/{role}', [RoleController::class, 'update']);
    Route::post('/roles/{role}/permissions', [RoleController::class, 'syncPermissions']);
    Route::delete('/roles/{role}', [RoleController::class, 'destroy']);
});
```

**Good**
```php
// database/seeders/RolePermissionSeeder.php — the ONLY place roles/permissions are written
class RolePermissionSeeder extends Seeder
{
    public function run(): void
    {
        $adminRole = Role::firstOrCreate(['name' => 'admin']);
        $editorRole = Role::firstOrCreate(['name' => 'editor']);

        $permissions = [
            'view-invoices', 'edit-invoices', 'delete-invoices', 'manage-users',
        ];
        foreach ($permissions as $permission) {
            Permission::firstOrCreate(['name' => $permission]);
        }

        $adminRole->syncPermissions($permissions);
        $editorRole->syncPermissions(['view-invoices', 'edit-invoices']);
    }
}

// deploy pipeline runs this on every deploy — idempotent via firstOrCreate/syncPermissions,
// safe to re-run without duplicating or silently dropping existing assignments
// php artisan db:seed --class=RolePermissionSeeder --force

// No RoleController, no PermissionController, no route exists for mutating
// roles/permissions at runtime — there is nothing to authorize because
// there is no endpoint to call.
```

**Checklist**
- [ ] No route or controller exists for creating, updating, or deleting roles or permissions at runtime, under any permission gate
- [ ] All role/permission definition and assignment happens via seeder classes, using idempotent calls (`firstOrCreate`, `syncPermissions`) safe to re-run on every deploy
- [ ] Role/permission slugs used for actor-type distinction (e.g. `admin`, `editor`) are checked explicitly by name — not inferred from an incidental numeric field (like a hierarchy "level" column) that wasn't designed to represent that distinction
- [ ] If the app later needs tenant-defined custom roles, that requirement is treated as a signal to redesign the authorization model — not a reason to add a narrow runtime endpoint next to the seeder-only setup
- [ ] A documented plan exists for migrating away from seeder-only if ever needed (how pre-existing runtime-created role/permission data, if any, would reconcile with seeder-defined ones)
