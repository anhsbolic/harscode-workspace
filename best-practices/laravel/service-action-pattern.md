# service-action-pattern.md

**Location:** `laravel/service-action-pattern.md`

**Principle**
Eloquent already implements Active Record — it merges data representation and data access (`where()`, `with()`, scopes, casts) in one place. A generic Repository layer (an interface + implementation per Model, wrapping `find()`/`all()`/`create()`) doesn't add abstraction value on top of that; it's indirection someone has to open during debugging for no benefit. The two classic justifications for it are weak in this ecosystem: "swap the ORM later" almost never happens in practice, and "mock it for testing" is worse than testing against a real Eloquent model with `RefreshDatabase`, which exercises relations/casts/scopes/events a mock can't. The actual problem Repository is usually reached for — a fat controller doing business orchestration — isn't a data-access problem, so a data-access abstraction doesn't fix it. Route reusable *queries* into Model scopes (they belong there naturally) and route *business orchestration* (multiple steps, validation, side effects) into single-purpose Action/Service classes — that's what actually empties out the controller.

**Bad**
```php
// A Repository that adds a class and an interface for zero behavior beyond Eloquent's own API
interface UserRepositoryInterface
{
    public function find(string $id): ?User;
    public function all(): Collection;
    public function create(array $data): User;
}

class UserRepository implements UserRepositoryInterface
{
    public function find(string $id): ?User
    {
        return User::find($id); // pure passthrough, no query logic, no behavior added
    }

    public function all(): Collection
    {
        return User::all();
    }

    public function create(array $data): User
    {
        return User::create($data);
    }
}

// Meanwhile the actual complexity lives inline in the controller anyway
class SubscriptionController extends Controller
{
    public function cancel(Request $request, string $id)
    {
        $subscription = Subscription::findOrFail($id);
        $subscription->status = 'cancelled';
        $subscription->cancelled_at = now();
        $subscription->save();

        $subscription->user->notify(new SubscriptionCancelledNotification());

        AuditLog::create([
            'action' => 'subscription_cancelled',
            'actor_id' => $request->user()->id,
            'target_id' => $subscription->id,
        ]);

        // ...more steps inline, controller keeps growing
    }
}
```

**Good**
```php
// Reusable query logic stays on the Model as a scope — no separate class needed
class Subscription extends Model
{
    public function scopeActive(Builder $query): Builder
    {
        return $query->where('status', 'active');
    }

    public function scopeExpiringWithin(Builder $query, int $days): Builder
    {
        return $query->where('expires_at', '<=', now()->addDays($days));
    }
}

// Business orchestration — multiple steps, a side effect, an audit trail — moves to an Action
class CancelSubscriptionAction
{
    public function execute(Subscription $subscription, User $actor): Subscription
    {
        $subscription->update([
            'status' => 'cancelled',
            'cancelled_at' => now(),
        ]);

        $subscription->user->notify(new SubscriptionCancelledNotification());

        AuditLog::create([
            'action' => 'subscription_cancelled',
            'actor_id' => $actor->id,
            'target_id' => $subscription->id,
        ]);

        return $subscription->fresh();
    }
}

class SubscriptionController extends Controller
{
    public function cancel(Request $request, Subscription $subscription, CancelSubscriptionAction $action)
    {
        return response()->json(
            $action->execute($subscription, $request->user())
        );
    }
}

// Tested against a real (test) database, not a mocked repository
class CancelSubscriptionActionTest extends TestCase
{
    use RefreshDatabase;

    public function test_cancelling_sets_status_and_notifies_user(): void
    {
        Notification::fake();
        $subscription = Subscription::factory()->create(['status' => 'active']);

        (new CancelSubscriptionAction())->execute($subscription, User::factory()->create());

        $this->assertEquals('cancelled', $subscription->fresh()->status);
        Notification::assertSentTo($subscription->user, SubscriptionCancelledNotification::class);
    }
}
```

**Checklist**
- [ ] No generic Repository interface+implementation exists whose methods are a 1:1 passthrough to Eloquent (`find`, `all`, `create`) with no added query logic or behavior
- [ ] Reusable, filtered queries live as query scopes on the Model (`scopeActive()`, `scopeExpiringWithin()`), not duplicated inline across controllers
- [ ] Any process with multiple steps, validation, or a side effect (notification, audit log, external call) lives in a single-purpose Action/Service class, not inline in the controller
- [ ] Action/Service classes are tested against a real test database (`RefreshDatabase`) exercising actual Eloquent behavior, not by mocking a repository interface
- [ ] A dedicated Query class is only introduced for a genuinely complex query reused across multiple distinct endpoints — not applied preventively to every Model "just in case"
