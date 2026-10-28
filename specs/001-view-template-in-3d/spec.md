# Feature 001: View a BTO template in 3D

**Status:** Approved by owner (2026-10-28)
**Created:** 2026-10-28
**Depends on:** nothing (first feature)

This spec says **what** the feature does and **why**. It deliberately says nothing about technology. That belongs in `plan.md`, written after this spec is approved.

## Summary

A homeowner picks a 4-room BTO template and sees it as an interactive 3D model in their browser. They can turn it around, zoom in, and see each room labelled. This is the foundation that themes, customisation and plan upload build on.

## Source plan

The template is based on an owner-provided HDB brochure image: "4-Room Floor Plan (With Suggested Furniture Layout)", approx. floor area 90 sqm, inclusive of an internal floor area of 86 sqm and an air-con ledge.

The image has **no dimensions**, so real-world sizes must be worked out by calibration (see open question 3). The suggested furniture drawn on the plan is ignored in this feature.

### What I read from the plan (confirmed by owner, 2026-10-28)

This reading was inferred from the image, so under Constitution P4 the owner confirmed it before it became the template.

| Space | Reached from | Notes |
|---|---|---|
| Living/Dining | Main entrance | Front door opens inward. A second outward-opening leaf looks like the gate. Includes the entrance area and the corridor to the bedrooms. |
| Household shelter | Living/Dining, near the entrance | Thick walls. Door opens into the living area. |
| Bedroom 2 | Living/Dining corridor | Left of the two "Bedroom" labels. |
| Bedroom 3 | Living/Dining corridor | Right of the two "Bedroom" labels. |
| Main bedroom | End of the corridor | Has its own bathroom. |
| Common Bath/WC | Living/Dining corridor | Left bathroom. |
| Main Bath/WC | Main bedroom | Right bathroom (en suite). |
| Kitchen | Living/Dining | **Appears open to the dining area (no wall drawn between them).** |
| Service yard | Kitchen | Through a door or opening at the kitchen's right side. Has a drying rack area. |
| Air-con ledge | None (outside the flat) | Next to the bathrooms. Counted in the 90 sqm but not in the 86 sqm internal floor area. |

Windows: along the top facade (living/dining, both bedrooms, main bedroom) and at the bathrooms and service yard. Structural columns: the solid black blocks, including the one projecting at the top centre and those at the corners.

## User scenarios

Stories are ordered by priority. Each one can be built and tested on its own.

### Story 1: See my flat type in 3D (P1)

As a homeowner who has booked a 4-room BTO flat, I want to see a 3D model of a typical 4-room layout so I can picture the space before collection.

**Independent test:** open the product, choose the 4-room template, and confirm a 3D model appears that can be rotated and zoomed.

**Acceptance scenarios**

1. **Given** I open the product, **when** I choose the 4-room template, **then** a 3D "dollhouse" view appears: walls at full height, no ceiling, viewed from above at an angle.
2. **Given** the 3D view is showing, **when** I drag (mouse) or swipe (touch), **then** the model rotates around its centre.
3. **Given** the 3D view is showing, **when** I scroll or pinch, **then** the view zooms in and out, staying within limits that keep the flat visible.
4. **Given** I have moved the view, **when** I choose "Reset view", **then** the original view is restored.
5. **Given** the 3D view is showing, **then** door openings and window openings are visible as gaps in the walls.

### Story 2: Know which room is which (P2)

As a homeowner, I want rooms labelled with their name and floor area so I can match the model to the HDB brochure.

**Independent test:** with the 3D view open, confirm every room shows a label with its name and area, and that labels can be hidden.

**Acceptance scenarios**

1. **Given** the 3D view is showing, **then** each room shows its name (for example "Master Bedroom") and floor area in square metres.
2. **Given** labels are showing, **when** I turn labels off, **then** all labels disappear, and turning them on brings them back.
3. **Given** I rotate the view, **then** labels stay readable (facing me, not mirrored or upside down).

### Story 3: Switch to a flat 2D plan (P3)

As a homeowner, I want a top-down plan view so I can compare the layout directly with my paper floor plan.

**Independent test:** switch to plan view and confirm it shows the same layout from directly above, with labels.

**Acceptance scenarios**

1. **Given** the 3D view is showing, **when** I choose "Plan view", **then** the camera moves to look straight down at the whole flat.
2. **Given** plan view is showing, **when** I choose "3D view", **then** the dollhouse view returns.

## Edge cases

- **Device cannot display 3D:** the product shows a plain message explaining the device or browser is not supported. It does not show a blank screen.
- **Small screens:** on a phone held upright, the whole flat fits on screen in the default view, and controls remain reachable with a thumb.
- **Template fails validation:** the template is not shown. Homeowners see a short apology. Developers see which invariant failed. This is caught by automated checks before release, so homeowners should never see it.
- **Slow connection:** a loading indicator shows until the model is ready.

## Requirements

### Functional requirements

- **FR-001** The product provides one 4-room BTO template.
- **FR-002** Each template is stored as layout data in a documented, machine-checkable format, in millimetres. (Constitution P2.)
- **FR-003** Layout data is checked against every invariant below before a model is generated. (Constitution P3.)
- **FR-004** The 3D model is generated from the layout data and includes:
  - walls with their real thickness and full floor-to-ceiling height,
  - door and window openings at the right positions, widths, heights and sill heights,
  - a floor surface for each room.
- **FR-005** Every generated surface is tagged with what it is (for example "bathroom floor", "bedroom wall", "kitchen wall") so that a later feature can restyle surfaces by type. This feature uses one neutral appearance for everything.
- **FR-006** Navigation supports mouse, trackpad and touch: rotate, zoom, pan, and reset view.
- **FR-007** Room labels show the room name and floor area calculated from the layout data, and can be toggled on and off.
- **FR-008** A visible note states that the mockup is indicative and not a substitute for official HDB plans or on-site measurement. (Constitution P6.)
- **FR-009** The product works in current versions of Chrome, Safari, Edge and Firefox, on desktop and mobile, with nothing to install.

### Layout invariants

These are the rules every layout must satisfy. They are the most important part of this spec to review: once approved, the validator enforces them on every layout from every source, including future uploads and auto-digitised plans.

| ID | Rule | Plain-language reason |
|---|---|---|
| INV-01 | Every wall has a length greater than zero, and a thickness within an allowed range. | Catches typos and zero-size walls. |
| INV-02 | Every door and window sits fully within its wall, and openings on the same wall do not overlap. | A door cannot hang off the end of a wall. |
| INV-03 | Every opening's top is below the ceiling, and every window's sill is above the floor. | Keeps openings physically possible. |
| INV-04 | Every room is a single closed outline that does not cross itself. | A room must have a clear inside and outside. |
| INV-05 | Rooms do not overlap each other. | Floor area cannot be counted twice. |
| INV-06 | The flat's internal area, measured the same way HDB measures it, is within a tolerance of the stated internal floor area (86 sqm for this template). External areas such as the air-con ledge are excluded. | Confirms the layout matches HDB's published size. |
| INV-07 | There is exactly one main entrance door. | Every flat has one front door. |
| INV-08 | Every internal room can be reached from the main entrance through doors or open connections. External areas (air-con ledge) are exempt. | Catches missing doors and isolated rooms. |
| INV-09 | There is exactly one household shelter, and all of its walls are marked as structural. | Shelter walls can never be removed. Later customisation relies on this flag. |
| INV-10 | Generating the model twice from the same layout gives identical results. | Deterministic output (Constitution P2). |

### Key entities

These are the things the layout data describes, in plain terms. Their exact format is decided in the plan.

- **Template:** a named, ready-made layout plus facts about it: flat type, stated internal floor area, source, and an "indicative" flag.
- **Layout:** the complete description of one flat: its walls, openings, rooms and ceiling height.
- **Wall:** a straight segment with a start point, end point, thickness, and a flag saying whether it is structural.
- **Opening:** a door or window in one wall, with position along the wall, width, height, and (for windows) sill height. Doors also record which way they swing and whether they are the main entrance.
- **Room:** an outline (polygon) on the floor, with a type (bedroom, bathroom, kitchen, living/dining, household shelter, service yard, and so on), a display name, and whether it is internal or external (the air-con ledge is external).
- **Open connection:** two rooms that join without a wall or door between them, such as the kitchen and dining area. It counts as a route for INV-08.
- **Column:** a solid structural block, usually at a corner or along the facade. Like structural walls, it can never be removed.

## Success criteria

Each criterion is measurable and gets checked before this feature is called done (Constitution P7).

- **SC-001** Someone who has never used 3D software can open the 4-room template and find every room within 1 minute, without help. Checked by watching at least 3 people try it.
- **SC-002** On a mid-range phone, the model becomes interactive within 5 seconds of choosing the template.
- **SC-003** Rotating and zooming feel smooth (at least 30 frames per second) on a mid-range phone.
- **SC-004** Wall positions, thicknesses and opening sizes in the 3D model match the layout data to within 1 mm.
- **SC-005** Every shipped template passes all invariants. This runs automatically on every change.
- **SC-006** For each invariant, a deliberately broken example layout is rejected, and the error names that invariant. This proves the validator actually catches each problem.

## Out of scope

Each item is planned as a later feature (see `specs/README.md`):

- interior themes and switching between them,
- moving or removing walls, and other customisation,
- furniture,
- fixed fittings shown on the plan (WC, basin, kitchen counter, stove, sink, shower zone, drying rack),
- the entrance gate as a separate leaf,
- uploading a floor plan, and automatic digitising,
- other flat types (2-room Flexi, 3-room, 5-room, 3Gen),
- eye-level walkthrough,
- exporting, saving or sharing,
- accounts and logins.

## Open questions

These need an answer before or during planning.

1. **[RESOLVED] Plan reading.** Owner confirmed the table, including the open kitchen and the en suite main bathroom.
2. **[RESOLVED] Default view.** Owner confirmed the dollhouse view as the default.
3. **[ADDRESSED IN PLAN] Scale calibration.** See plan section 3.3. Calibrated from independent references, with the 86 sqm kept back as the check.
4. **[ADDRESSED IN PLAN] How HDB measures internal floor area.** See plan section 3.2. The ledge is excluded (HDB source). Whether walls and the shelter count is recorded as assumption A-1.
5. **[ADDRESSED IN PLAN] INV-06 tolerance.** 3%, to be confirmed against this template.
6. **[NEEDS CLARIFICATION] Source file.** Please save the original plan file into `reference/plans/`. I can see the image in chat but can't save it from there. It is HDB's brochure artwork, so it stays out of a public GitHub repo (excluded from git).

## Review checklist for the owner

- [ ] The summary describes what you want homeowners to get from this first feature.
- [ ] The priorities make sense: 3D view first, labels second, plan view third.
- [ ] Every invariant is a rule you agree must always hold.
- [ ] The success criteria are things you would actually accept as "done".
- [ ] Nothing in "Out of scope" needs to move into this feature.
- [ ] Open questions 1, 2 and 6 are answered.
