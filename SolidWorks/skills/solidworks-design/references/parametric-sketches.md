# Precise Parametric Sketches

Use for analytic profiles, small radii, traced logos, or sketches distorted by automatic inference.

## Preserve the intended geometry

- Build circles and circular arcs as native entities, not chains of short segments. Use splines where the intended shape actually requires them.
- Establish the sketch-to-model transform from the selected plane or face. Do not infer world axes from a plane's display name. Confirm a small pilot sketch and feature before constructing a large pattern.
- Automatic snapping can move endpoints or alter a small arc even when entity creation reports success. Read back endpoints, centers, radii, and connection gaps before continuing.
- When COM fallback is permitted, temporarily set `SketchManager.AddToDB = True` for deterministic insertion. Optionally disable `DisplayWhenAdded` during a batch. Record and restore both prior values in `finally`; redraw afterward. Bypassing inference also means explicitly creating the intended relations.
- Add coincident endpoint relations, applicable horizontal/vertical relations, tangency, concentricity, equality, and driving dimensions to express design intent. Visually touching endpoints are not evidence of a coincident relation.

## Define without distorting

- Establish intended relations before adding the remaining dimensions. Dimension critical arc radii explicitly. Adding inferred relations after automatic dimensioning can overconstrain a previously solved sketch.
- Prefer meaningful dimensions and relations over blanket Fix constraints. Fixing all entities hides missing design intent and makes later editing difficult.
- `FullyDefineSketch` needs a reliable datum. Supply explicit datums or select the sketch origin as `EXTSKETCHPOINT` with the appropriate horizontal/vertical datum marks for the installed API. Verify selection and API constants before calling it.
- An automatic define operation may omit zero-valued dimensions. If a point belongs on a sketch axis, express that with a point-axis relation instead of repeatedly requesting automatic dimensions.
- Remove unnecessary collinear splits in a straight contour, or deliberately locate the intermediate point. Such a point can remain free to slide even when the contour looks complete.
- A success return from the defining operation does not prove the resulting sketch is fully constrained. Read `ISketch.GetConstrainedStatus` using the installed enumeration, then check for overconstraint, unresolved degrees of freedom, and invalid geometry.

## Inspect the result

After relations, dimensions, and rebuild, compare actual radii, endpoint positions, tangent directions, and closed-loop connectivity with the design intent. Check minimum gaps and concave radii where a cutter must fit. Inspect a normal view and an oblique view for the relevant faces.

Distinguish display tessellation from geometric defects: graphics quality may change visible faceting, but cannot repair a wrong radius, unintended kink, or open contour.
