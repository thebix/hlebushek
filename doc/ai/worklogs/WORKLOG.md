# Worklog

This file describes the worklog concept. 

Worklog - is an md file that AI agent evolve working on the feature of the product.

Worklogs solve three problems:
- Context restoration - AI sessions end, worklogs persist
- Auditability — what decisions were made and why
- Scope control — explicit milestones prevent gold-plating

## Worklog file Format

Here’s a complete worklog example with all the sections. Most features only need a subset.

```
# Feature: User Registration Rate Limiting

## Skills Loaded
- `/api-patterns` — touches API response headers
- `/rate-limiting` — reuses existing middleware

## Milestones
- [ ] M1: Write failing tests for rate limit violations
- [ ] M2: Implement rate limiting

## Invariants (high-stakes features only)
- **INV-1:** A single email cannot receive >5 magic links per hour
- **INV-2:** A single IP cannot request >10 magic links per hour

## Closing the Loop
- [ ] Run `npm test` — all rate limit tests pass
- [ ] Playwright: hit endpoint 6 times, verify 429 on 6th
- [ ] Edge case: verify error message displays correctly

## Session Log
### Session 1 (2026-01-08)
- Completed M1
- **Next:** Implement rate limiting

## Surprises
- Discovered existing rate limiter in `/lib/rate-limit.ts` — reusing instead of building new
```

- Skills Loaded: primes context before coding
- Milestones: prevent scope creep
- Invariants define what MUST be true
- Closing the Loop: is how to verify the work actually works
- Session Log: enables context restoration
- Surprises: capture what was learned

## Naming convention

Use `WORKLOG_feature-name_YYYY-MM-DD.md`.
Files must be placed in [worklogs](./) folder

## Size

Before starting work, calibrate:

- Worklog is longer than 100 lines for a simple task → Cut sections, not detail
- More than 5 commits planned → Merge related changes
- “TBD” or placeholder dates → Fill in or delete
- Invariants for a UI-only change → Delete the Invariants section
- You’re proud of how thorough it looks → You’ve over-engineered it
- The rule: 50–100 lines for most features. If your worklog is longer than your implementation will be, cut it down.
