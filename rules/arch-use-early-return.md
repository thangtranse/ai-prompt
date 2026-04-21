---
title: Use Early Return to Reduce Nesting
impact: HIGH
impactDescription: Makes control flow easier to read
tags: architecture, control-flow, readability
---

## Use Early Return to Reduce Nesting

Use guard clauses to exit early for invalid, empty, or unsupported cases. This keeps the main execution path flat and readable. Early return is preferred over deep nesting, but it should be used deliberately. Keep the function focused and avoid scattering many unrelated return points.

**Incorrect (deep nesting hides the happy path):**

```typescript
function getDiscountPrice(order?: Order): number {
  if (order) {
    if (order.items.length > 0) {
      if (order.customer.is_premium) {
        return order.total * 0.9;
      }
    }
  }

  return 0;
}
```

**Correct (guard clauses expose the happy path):**

```typescript
function getDiscountPrice(order?: Order): number {
  if (!order) {
    return 0;
  }

  if (order.items.length === 0) {
    return 0;
  }

  if (!order.customer.is_premium) {
    return 0;
  }

  return order.total * 0.9;
}
```

Reference: [Refactoring Guru - Replace Nested Conditional with Guard Clauses](https://refactoring.guru/replace-nested-conditional-with-guard-clauses)
