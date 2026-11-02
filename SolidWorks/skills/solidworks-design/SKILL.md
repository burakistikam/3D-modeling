---
name: solidworks-design
description: Create, modify, inspect, or validate SolidWorks parts and assemblies while preserving editable features, configurations, and mates. Use for design work; technical drawings require a separate drawing workflow.
---

# SolidWorks Design

Preserve the user's dimensions, production method, file scope, and existing
component transforms unless the current request changes them. This portable
edition contains general methods, without a machine-specific plugin or review gate.

## Access

1. If a SolidWorks MCP server is available, probe it directly with its status tool;
   do not infer availability from window discovery. Inspect the actual tool schema.
2. If MCP is absent or a direct call fails, report that limitation. Use an available
   local COM interface only when needed; read [COM fallback](references/com-fallback.md).
3. Confirm the target document and configuration before mutation. Keep temporary
   helpers and measurements in the private task workspace, outside this public repo.

## Modeling

- Default to MMGS unless the user specifies another unit system; independently
  check the units expected by each API call.
- Use clear English entity names and editable native features. Keep sketches as
  fully defined as practical; check actual geometry as well as constraint status.
- Prefer native lines, circles, and tangent arcs for analytic geometry. For precise
  profiles or inference problems, read [parametric sketches](references/parametric-sketches.md).
- Preserve original positions in a reference configuration when relevant. Use
  configuration-specific mates or dimensions for requested motion.
- Reuse part definitions for repeated hardware. Prefer Toolbox or verified standard
  hardware; mark simplified hardware `ENVELOPE_ONLY` in names or custom properties.
- For relief, opposing-face details, or V grooves, read [CNC engraving](references/cnc-engraving.md).
  Derive dimensions and cutter assumptions from the current request.
- For printed grippers or fixtures, read [FDM guidance](references/fdm-gripper.md).

## Delivery

For a saved-model change, follow the [delivery checklist](references/delivery-checklist.md).
Leave the requested configuration active, intended components resolved and visible,
and the saved viewport showing the result. Rebuild, read back errors and warnings,
save, and check the document's dirty state.

When the MCP exposes them, use explicit `rebuild_document`,
`check_errors(rebuild_first=true)`, and `get_active_document_info` calls against
the verified target. A save hook or write script success message does not replace
final readback. Use the available screenshot tool when visual state is relevant.

Use a separate Worker/Reviewer only when the user or applicable workspace rules
require it. Otherwise validate through a separate readback step and state that no
independent agent review occurred. This skill does not authorize additional agents
or external publication. Keep CAD paths and task evidence in the private task report.
