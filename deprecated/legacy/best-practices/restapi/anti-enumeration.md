# anti-enumeration.md

**Location:** `restapi/anti-enumeration.md`

**Principle**
Endpoints that could leak the existence of an account/resource through a difference in response (e.g. register, forgot-password) must return a generic response that's identical regardless of whether the account/resource exists. Additionally, any comparison against a secret (token, password hash, signature) must use constant-time comparison — even a small difference in comparison execution time can become a side-channel that gradually leaks secret information.

**Bad**
```go
func ForgotPassword(email string) error {
    user := repo.FindByEmail(email)
    if user == nil {
        return errors.New("email not found") // different response = enumeration
    }
    sendResetEmail(user)
    return nil
}
// token comparison
if providedToken == storedToken { ... } // non-constant-time comparison
```

**Good**
```go
func ForgotPassword(email string) error {
    user := repo.FindByEmail(email)
    if user != nil {
        sendResetEmail(user)
    }
    return nil // generic success response, regardless of whether the user was found
}
// token/secret comparison
if subtle.ConstantTimeCompare([]byte(providedToken), []byte(storedToken)) == 1 { ... }
```

**Checklist**
- [ ] Register/forgot-password/similar endpoints return an identical generic response regardless of account existence
- [ ] Every comparison against a secret (token, hash, signature) uses constant-time comparison
- [ ] Response timing on sensitive endpoints doesn't differ significantly between "found" and "not found" (avoid an early return that skips an expensive operation on only one branch)
- [ ] Error messages don't leak internal details that aid enumeration (e.g. distinguishing "wrong password" from "user not found")