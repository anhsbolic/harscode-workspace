# decimal-and-money.md

**Location:** `go/decimal-and-money.md`

**Principle**
Monetary values must never pass through `float64` at any point in the flow — rounding error in float accumulates and is not reversible. Use a decimal type (`shopspring/decimal` or equivalent) end-to-end: from input parsing, through storage, to calculation. Rounding mode must be explicit and consistent (don't mix `Round()` in one place and `Truncate()` in another for calculations that relate to each other). Comparing two decimal values must use the `.Equal()` method, not the `==` operator — two decimal representations can be mathematically equal while having different underlying structs (different scale).

**Bad**
```go
amount, _ := strconv.ParseFloat(input, 64)
total := amount * 1.11 // tax calculation through float64
if total == expectedTotal { ... } // float equality, almost always wrong
```

**Good**
```go
amount, err := decimal.NewFromString(input)
if err != nil { return fmt.Errorf("invalid amount: %w", err) }
tax := amount.Mul(decimal.NewFromFloat(0.11)).Round(2) // explicit rounding mode
total := amount.Add(tax)
if total.Equal(expectedTotal) { ... }
```

**Checklist**
- [ ] No `float64` anywhere along a path that touches money (parsing, calculation, storage, response)
- [ ] Rounding mode (`Round`/`Truncate`/`Ceil`/`Floor`) is consistent across calculations that relate to each other
- [ ] All decimal value comparisons use `.Equal()`, not `==`
- [ ] Database column precision/scale matches the precision used in the application layer