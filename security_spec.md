# Security Specification: Clepto Trap

## 1. Data Invariants
- A `SecurityEvent` must always belong to a specific `userId`.
- A `SecurityEvent` must have a valid `type` (shoplifting, fall, suspicious, error, normal).
- The `timestamp` must be the server time of creation.
- Only the owner of the `userId` can create or read events in their subcollection.
- Events are immutable once created (audit integrity).

## 2. The "Dirty Dozen" Payloads (Denial Tests)

1. **Identity Spoofing**: Attempt to create an event in user B's collection as user A.
2. **Path Poisoning**: Attempt to access `/users/!!junk!!/events/event1`.
3. **Ghost Field Injection**: Attempt to create an event with an extra `isVerified: true` field.
4. **Invalid Type**: Attempt to create an event with `type: 'celebration'`.
5. **Timestamp Fraud**: Attempt to create an event with a client-side `timestamp`.
6. **Confidence Overflow**: Attempt to create an event with `confidence: 1.5`.
7. **Size Attack**: Attempt to create an event with a 10MB `imageUrl`.
8. **Description Overflow**: Attempt to create an event with a 100KB `description`.
9. **Unauthorized List**: Attempt to list events for a different user.
10. **Unauthorized Get**: Attempt to get a specific event ID for a different user.
11. **Forbidden Update**: Attempt to update an existing event's `type`.
12. **Forbidden Delete**: Attempt to delete a security log.

## 3. Test Runner (Conceptual)
A `firestore.rules.test.ts` would verify that all the above 12 scenarios return `PERMISSION_DENIED`.
Since I cannot run complex test suites here easily, I will focus on the hardened rule implementation.
