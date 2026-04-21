---
title: Use Meaningful Names
impact: HIGH
impactDescription: Speeds up code review and lowers misunderstanding
tags: architecture, naming, readability
---

## Use Meaningful Names

Variable, function, and parameter names must communicate purpose clearly. Avoid vague names such as `data`, `value`, `temp`, or short abbreviations unless they are obvious, standard, and local in scope. Reviewers should understand intent without reverse-engineering the code.

**Incorrect (ambiguous names and abbreviations):**

```typescript
async function procUsr(lst: User[]) {
  const rs = [];

  for (const i of lst) {
    if (i.stt === 'A') {
      rs.push(i);
    }
  }

  return rs;
}
```

**Correct (explicit names with domain meaning):**

```typescript
async function filterActiveUsers(users: User[]) {
  const activeUsers: User[] = [];

  for (const user of users) {
    if (user.status === 'ACTIVE') {
      activeUsers.push(user);
    }
  }

  return activeUsers;
}
```

Reference: [Clean Code Summary - Meaningful Names](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29)
