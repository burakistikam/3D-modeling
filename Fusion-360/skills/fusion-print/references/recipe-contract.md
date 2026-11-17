# Recipe and reference contract

This describes the existing local runtime, not a model specification. Runtime code
and task inputs remain outside the management repository.

## Files and functions

`models/<part>/model.json` contains source dimensions and requirements;
`models/<part>/recipe.py` contains geometry. The recipe path in JSON is relative
to `models/`, for example `<part>/recipe.py`.
The JSON requires `schema_version: 1`, `units: "mm"`, a nonempty `name`,
`recipe`, `parameters`, and `requirements`.

Requirements include positive integer `body_count`, three positive values each
for `expected_size_mm` and `build_volume_mm`, and positive
`dimension_tolerance_mm`. Optional `expected_bounds_mm` has finite three-value
`min` and `max` vectors in root coordinates. Each max exceeds min; their
difference must match expected_size_mm within tolerance. Derive expected bounds
from design intent, not from the produced geometry.

| Function | Execution | Contract |
|---|---|---|
| validate(parameters) | CLI and before build | Reject invalid parameters without CAD mutation |
| build(context, parameters) | Fusion main thread | Construct features in the new target document |
| inspect(context, parameters) | Fusion main thread | Read geometry and return a nonempty map of check names to booleans |

Any false check fails the CAD gate. Measurement numbers or prose cannot replace
boolean results; write detailed measurements to a separate task report.

Context provides `app`, `design`, `output`, and `references`;
`component` returns `design.rootComponent`. The output directory belongs to
that job. Importing the standalone recipe must not call adsk or have side effects;
do not use relative imports. Review untrusted recipes before executing Python.

## Spatial checks

Use actual sketch/model transformations for rotated planes, not guessed axis signs.
Fusion Point3D lengths are cm; convert mm inputs explicitly. Check profile count
before selecting an index and select join/cut targets explicitly. After topology
changes, identify faces/edges again using geometry, position and direction.

Check root min/max positions after the first sketch/extrusion and in final inspection.
A correct overall size does not prove correct orientation, holes, overlap or walls.
The standard gate supports root bodies; assemblies require a separate authorized
inspection rather than bypassing that limitation.

## Reference records

Each optional references entry identifies an image relative to `references/`:

```json
{
  "path": "part/front.png",
  "source": "User-provided front photograph",
  "notes": "Two visible holes; perspective and hidden rear face are uncertain.",
  "calibration": {
    "known_distance_mm": 40,
    "pixel_points": [[120, 180], [520, 180]]
  }
}
```

Calibration is optional. Two known pixel points produce mm/pixel; this does not
correct perspective or calibrate a Fusion canvas. Distinguish supplied dimensions
from visual estimates. `context.add_canvas(0)` adds an uncalibrated guide;
verify canvas scale separately when needed. Images and hashes are snapshotted with
job inputs. Do not invent a reference when none was supplied.

## Verification limits

A valid JSON/recipe is not verified CAD. Compare the final CAD bounds to the intended
frame, and mesh bounds to that job's CAD measurements. Matching envelopes do not
replace internal geometry checks. inspect-mesh reports failure on incomplete or
invalid inputs; if its report cannot be written, report the IO failure. These reports
describe one inspection, not continuous monitoring of later file changes.
