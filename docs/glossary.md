# Glossary

Plain-language meanings of terms used in this project. New terms are added when they first appear.

## Process

- **Spec (specification):** a written description of what a feature must do and how we'll know it works. It says nothing about how it is built.
- **Constitution:** the project-wide rules every feature must follow.
- **Plan:** the technical design for one feature: which tools, which data format, and why.
- **Acceptance scenario:** a concrete check written as "Given (situation), when (action), then (expected result)". If it passes, that piece of behaviour works.
- **Success criterion:** a measurable target, such as "interactive within 5 seconds", that decides whether a feature is done.
- **Invariant:** a rule that must always be true of the data, such as "rooms don't overlap". The validator checks invariants automatically.
- **Validator:** code that checks data against the invariants and rejects anything that breaks them.
- **Negative test:** a test that feeds in deliberately bad data and checks it gets rejected. It proves the validator really catches the problem.
- **Held-out test set:** examples kept aside and never used while building or tuning, so they give an honest measure of accuracy.
- **Differential testing:** comparing a new output against a trusted reference, such as an auto-digitised plan against a hand-traced one.
- **Deterministic:** the same input always gives exactly the same output.
- **Source of truth:** the one place a fact is stored. Everything else is derived from it.

## Floor plans and HDB

- **BTO (Build-To-Order):** HDB's flat sales scheme, where flats are built after buyers book them.
- **Internal floor area:** the floor area HDB publishes for a flat. Exactly what it includes (walls, shelter, ledge) is being confirmed.
- **Household shelter:** a reinforced room required in new flats. Its walls, floor and ceiling must not be altered.
- **Structural wall / column:** part of the building's frame that holds it up. It can never be removed. Non-structural walls (partitions) can sometimes be removed with approval.
- **Air-con ledge:** an external platform for air-conditioner units. Counted in the approximate floor area, but not part of the living space.
- **Opening:** a gap in a wall for a door or window.
- **Sill height:** the height from the floor to the bottom of a window.

## 3D

- **Dollhouse view:** a 3D view from above at an angle, with the ceiling removed so you can see into every room.
- **Plan view:** looking straight down at the flat, like a paper floor plan.
- **Calibration:** working out real-world size from a drawing without dimensions, using something of known size.
- **WebGL:** the browser feature that lets web pages draw 3D graphics using the device's graphics chip.
- **Mesh:** a 3D shape made of many small triangles.
- **Extrusion:** turning a flat 2D outline into a 3D solid by raising it to a height.
- **Polygon boolean operations (clipping):** combining flat shapes: union (merge), difference (cut one out of another), intersection (the overlap).
- **Z-fighting:** flickering when two surfaces sit in exactly the same place and the screen can't decide which to draw.
- **glTF / GLB:** the standard file format for 3D models on the web, like JPEG for 3D.

## Software

- **Dependency:** code written by someone else that the project uses. A runtime dependency ships to users. A development dependency is only used to build and test.
- **Package manager (npm):** the tool that downloads dependencies and records their exact versions.
- **Pinning:** recording an exact version, so everyone gets the same code and an unexpected update can't slip in.
- **Type checking (TypeScript):** checking, before the code runs, that data is used consistently, for example that a wall's thickness is always a number.
- **Bundler / dev server (Vite):** combines source files into a few small files for publishing, and serves the site locally while you work, reloading on every change.
- **Pipeline:** a design where data passes through a series of steps, each with one job, in one direction.
- **Dependency isolation (wrapper):** calling a library only through our own small module, so it can be swapped by changing one file.
- **Unit test:** a fast automated test of one small piece of code.
- **Property-based test:** a test that generates many random inputs and checks a rule holds for all of them.
- **End-to-end (E2E) test:** a test that drives a real browser like a user would: clicking, dragging, reading the screen.
- **CI (continuous integration):** automated checks that run on every change pushed to GitHub.
- **LTS (long-term support):** a release line that gets fixes for years. Preferred for anything that must stay stable.
