# CNC Relief and V Engraving

Use for milled relief, engraved outlines, and details on opposing faces. Keep manufacturing dimensions specific to the current request; do not carry over a previous part's size, depth, tool angle, or artwork.

## Geometry and cutter assumptions

- Distinguish the cutter's included angle from its half-angle. For an ideal sharp symmetric V cutter, groove mouth width is `w = 2 * d * tan(theta / 2)`, where `d` is penetration and `theta` is the included angle. Record a sharp-tip assumption when actual tip geometry is unknown.
- Derive depth and spacing together. Verify the chosen section against the tool's actual tip geometry when supplied; a nominal angle alone does not describe a flat or rounded tip.
- Represent requested engraving as physical subtractive geometry. A visible sketch or a flat-bottom thin cut is not a V groove.
- For relief, determine whether raised features are retained stock above a pocket floor. Check the total envelope, including the relief, against the requested overall thickness.
- Check remaining material between opposing cuts. A front relief and a rear engraving share the same stock thickness.
- For end-milled pockets, account for cutter access, minimum channel width, and concave radii of at least the tool radius plus any deliberately chosen clearance. Explain functional machining radii; do not add unrelated cosmetic edge finishing.

## Native feature strategies

- Circular V grooves can use a revolved triangular cut section.
- Line-and-arc engraving paths can use a swept triangular cut section. Put the section in a plane normal to the initial path tangent, correctly positioned at the surface and directed into the stock.
- Open paths may need a conical end cut to represent the V tool's endpoint footprint. Inspect sweep ends and intersections rather than assuming the sweep alone reproduces the cutter envelope.
- Check a representative cut before building all paths. Inspect depth, mouth width, orientation, continuity, and body count. If a feature method fails repeatedly, inspect the failure and choose a documented alternative instead of varying API arguments blindly.
- On the opposite face, verify text and artwork from the viewer looking at that face. A sketch-coordinate transform can reverse lettering even when the profile appears correct from the original side.

## Delivery scope

Verify groove sections, stock thickness, relevant residual thickness, spacing, and tool access on the final geometry. Distinguish CAD checks from CAM toolpath or machine simulation. Do not claim machining readiness from solid-body validity alone. Supply cutting speeds or feeds only when requested.
