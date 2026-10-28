# Project Constitution

**Status:** Approved by owner (2026-10-28)
**Version:** 1.0.0
**Last amended:** 2026-10-28

The constitution holds the rules that apply to every feature. Feature specs, plans and code must not contradict it. If a feature needs to break a rule, amend the constitution first, on purpose, and record why.

## Purpose

Give Singapore HDB BTO homeowners a quick, believable 3D mockup of their flat that they can restyle in different interior themes, without installing software or learning 3D tools.

## Principles

### P1. The spec comes before the code

Every feature starts as a written spec (what and why) that the owner approves. Only then do we write a plan (how), tasks, and code. When behaviour needs to change, the spec changes first and the code follows.

*Why:* code is cheap to produce and expensive to trust. A short spec is the cheapest thing for a human to review.

### P2. Layout data is the single source of truth

A flat is described once, as structured layout data in real-world millimetres. Every view (2D plan, 3D model, exports) is generated from that data. Nobody edits the 3D model directly. Generation is deterministic: the same layout and theme always produce the same model.

*Why:* one source of truth means one thing to validate, store and version. Derived outputs can always be thrown away and regenerated.

### P3. Validate everything at the door

All layout data passes the same validator before use, whatever its source: built-in templates, manual edits, uploaded plans, or automatic digitising. The validator checks the invariants (rules that must always hold) defined in the specs. Invalid data is rejected with a message that names the broken rule.

*Why:* a single checkpoint is easier to trust than many scattered checks.

### P4. Inferred data needs human confirmation

Anything the system guesses, such as walls detected from a plan image or AI-suggested layouts, is shown as a proposal. It becomes trusted layout data only after the homeowner confirms it.

*Why:* an extracted layout describes the picture it came from, including its mistakes.

### P5. Homeowner first

- Runs in a web browser on phone or computer. Nothing to install.
- No 3D, CAD or design knowledge needed.
- Sensible defaults, few choices per screen, plain language.

### P6. Honest about accuracy

Mockups are indicative. The product always says that it is not a substitute for official HDB plans or on-site measurement. Guidance about HDB renovation rules is informational, not approval.

### P7. A feature is done when its checks pass

Each feature has acceptance scenarios and measurable success criteria in its spec. A feature is complete only when they pass. Automated checks run on every change. Accuracy-sensitive features, such as automatic digitising, keep a held-out test set that is never used while tuning.

When a check fails, decide deliberately which artifact is wrong: the code, the spec, or the test. Fix that one.

### P8. Every dependency earns its place

Each new library, tool or external service is proposed in the feature plan with what it does, why it is needed, and the alternatives considered. The owner approves it before it is added.

### P9. Homeowners' data stays theirs

Uploaded floor plans, unit numbers and addresses are personal data. They are not sent to third-party services without the homeowner's explicit consent, and are not kept longer than the homeowner wants.

## Governance

- The owner approves the constitution and every feature spec.
- Amendments bump the version: major for removing or redefining a principle, minor for adding one, patch for wording.
- Each amendment updates **Last amended** and gets a line in the changelog below.

## Changelog

- 1.0.0 (2026-10-28): approved by owner.
- 0.1.0 (2026-10-28): first draft.
