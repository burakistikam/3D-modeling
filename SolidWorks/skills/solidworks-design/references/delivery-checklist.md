# SolidWorks delivery checklist

Use after a saved-model change. Report applicable checks against the final document;
mark missing checks explicitly. Evidence stays in the private task report.

## Document and part

- Confirm target document identity, type, units, configuration, and revision.
- Rebuild, read back errors and warnings, save, and confirm the document is clean.
- Query actual solid-body count, critical dimensions, feature state, and placements.
- For tight envelope checks, do not treat `GetPartBox` or `GetBodyBox` as exact
  extrema. Where needed, query `IBody2.GetExtremePoint` in both directions of each
  relevant axis for each body and compare against native dimensions.
- Check modified sketch constraints and actual radii, endpoints, and tangencies.
  Fully defined status alone does not prove the intended shape.
- Check physical holes, counterbores, clearances, and contact surfaces. For relief
  or grooves, use [CNC engraving](cnc-engraving.md) to inspect cut sections and stock.
- Refresh requested exports and reports after the final revision. Label earlier
  evidence by revision; do not present it as proof of modified geometry.

## Assembly and hardware

- Leave the requested configuration active and intended components resolved,
  unsuppressed, and visible. Confirm reference and target transforms.
- Check interference, intended contact, mounting alignment, and duplicate components.
  Distinguish an intended contact from unwanted overlap.
- Verify hardware standard, diameter, length, quantity, axis, and seat; check head
  access, grip length, thread engagement, and blind-hole bottom clearance.
- Mark simplified purchased parts `ENVELOPE_ONLY`.
- Redraw and zoom to fit; inspect a screenshot when visibility is part of acceptance.

## Evidence and review

Read the saved model independently of the write script's success response. A
separate reviewer, when required by the current task, should inspect without
changing CAD geometry. Do not invent a reviewer or a local gate that does not exist.

Report: actual access method; target file in the private workspace; active
configuration; rebuild errors/warnings; saved/dirty state; critical dimensions;
component, visibility, transform, and interference checks; hardware checks; export
revision; assumptions; unresolved items; and whether independent review occurred.

Use PASS only for verified applicable acceptance criteria. If blocked, identify the
specific missing evidence. If no CAD change was made, state that explicitly.

## Optional local evidence gate

If an installed plugin requires a structured Worker/Reviewer record, report the
same verified checks above as SOLIDWORKS_EVIDENCE with result, role, access,
cad_path, rebuild_errors, rebuild_warnings, dirty, and active_configuration.
For assemblies include component, visibility, transform, interference and hardware
results. A Reviewer also reports independent_review=true and
reviewer_changed_files=none. Missing evidence means FAIL or BLOCKED with a reason,
not an invented passing value. A no-CAD review states cad_changes=none and why.

For MCP-based CAD delivery, explicitly call rebuild_document,
check_errors(rebuild_first=true), and get_active_document_info on the target.
For a COM-only gate, print SOLIDWORKS_COM_EVIDENCE from separate readback, with
the verified CAD path, errors, warnings, dirty state and active configuration.
A local gate does not itself authorize spawning agents or changing CAD scope.
