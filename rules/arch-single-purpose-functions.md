---
title: Keep Functions Single Purpose
impact: HIGH
impactDescription: Reduces complexity and improves testability
tags: architecture, functions, maintainability
---

## Keep Functions Single Purpose

Each function should do one job well. If a function validates input, transforms data, persists records, sends notifications, and formats responses at the same time, it is doing too much. Prefer one main return for the happy path. Allow at most one additional early return when it materially reduces nesting and keeps the function easier to read.

**Incorrect (multiple responsibilities in one function):**

```typescript
async function createOrder(input: CreateOrderInput) {
  if (!input.items.length) {
    return { error: 'Order items are required' };
  }

  const total = input.items.reduce((sum, item) => sum + item.price, 0);
  const order = await orderRepository.save({ ...input, total });
  await mailService.sendOrderCreatedEmail(order.customer_email);

  return {
    id: order.id,
    total: order.total,
    message: 'Order created successfully',
  };
}
```

**Correct (split responsibilities into focused functions):**

```typescript
function validateOrderItems(items: OrderItem[]): void {
  if (items.length === 0) {
    throw new Error('Order items are required');
  }
}

function calculateOrderTotal(items: OrderItem[]): number {
  return items.reduce((sum, item) => sum + item.price, 0);
}

async function createOrder(input: CreateOrderInput): Promise<Order> {
  validateOrderItems(input.items);

  const total = calculateOrderTotal(input.items);

  return orderRepository.save({ ...input, total });
}
```

Reference: [Martin Fowler - Long Method](https://refactoring.com/catalog/extractFunction.html)
