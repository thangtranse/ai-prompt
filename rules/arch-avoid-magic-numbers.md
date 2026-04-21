---
title: Avoid Magic Numbers
impact: HIGH
impactDescription: Improves readability and reduces change risk
tags: architecture, readability, maintainability
---

## Avoid Magic Numbers

Do not leave unexplained numeric literals inside business logic. Extract them into named constants that communicate intent, units, and domain meaning. This makes code easier to review, safer to change, and less error-prone.

**Incorrect (hard-coded numbers with unclear meaning):**

```typescript
async function lockAccount(failedAttempts: number, lastAttemptAt: number) {
  if (failedAttempts >= 5 && Date.now() - lastAttemptAt < 300000) {
    throw new Error('Account locked');
  }
}
```

**Correct (named constants with clear intent):**

```typescript
const MAX_FAILED_LOGIN_ATTEMPTS = 5;
const ACCOUNT_LOCK_WINDOW_MS = 5 * 60 * 1000;

async function lockAccount(failedAttempts: number, lastAttemptAt: number) {
  const isLockedByAttempts = failedAttempts >= MAX_FAILED_LOGIN_ATTEMPTS;
  const isWithinLockWindow =
    Date.now() - lastAttemptAt < ACCOUNT_LOCK_WINDOW_MS;

  if (isLockedByAttempts && isWithinLockWindow) {
    throw new Error('Account locked');
  }
}
```

Reference: [Refactoring Guru - Replace Magic Number with Symbolic Constant](https://refactoring.guru/replace-magic-number-with-symbolic-constant)
