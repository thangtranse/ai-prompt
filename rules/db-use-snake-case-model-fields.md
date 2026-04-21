---
title: Use snake_case for Model and Collection Fields
impact: MEDIUM
impactDescription: Improves persistence-layer consistency
tags: database, naming, models, collections
---

## Use snake_case for Model and Collection Fields

For fields declared in models, entities, schemas, or collection documents, prefer `snake_case` naming so the persistence layer stays consistent and predictable. Keep this rule focused on storage-facing names. Application-local variables should still follow the conventions of the language and project.

**Incorrect (mixed and inconsistent field naming):**

```typescript
@Entity('user_profiles')
export class UserProfileEntity {
  @Column()
  firstName: string;

  @Column()
  lastLoginAt: Date;

  @Column()
  isActive: boolean;
}
```

**Correct (storage-facing fields use snake_case consistently):**

```typescript
@Entity('user_profiles')
export class UserProfileEntity {
  @Column({ name: 'first_name' })
  first_name: string;

  @Column({ name: 'last_login_at' })
  last_login_at: Date;

  @Column({ name: 'is_active' })
  is_active: boolean;
}
```

Reference: [PostgreSQL Lexical Structure](https://www.postgresql.org/docs/current/sql-syntax-lexical.html)
