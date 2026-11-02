# FDM Gripper and Fixture Guidance

Use this reference for 3D-printed grippers, fingers, nests, and fixtures.

## Inputs

Evaluate part mass, acceleration, grip direction, contact geometry, print process, material, layer orientation, friction, tolerance, and safety factor. Ask the user only when a missing value can materially change geometry or strength. Mark unresolved production material as `TBD` and do not call the design production-ready.

## Geometry

- Use broad contact areas and short load paths where practical.
- Avoid sharp internal corners; add printable radii or chamfers.
- Add mechanical capture only where it does not jam the workpiece during approach or release.
- Treat 0.30–0.50 mm as a starting range for ordinary FDM clearance, not a universal value. Adjust for printer, material, orientation, and fit purpose.
- Orient layers so primary bending and fastener loads do not rely on weak inter-layer tension when practical.

## Fasteners

- Verify printed stack thickness beneath the screw head.
- Calculate usable thread engagement in the metal jaw or insert.
- Keep the screw tip clear of the cylindrical bottom and drill-tip region of a blind hole.
- Check counterbore access for the actual driver and head geometry.

## Gripping configurations

Preserve the fully closed or initial jaw state as a reference configuration. Create the target grip state with configuration-specific motion. Validate intended contact at the target position and clearance during approach and release.
