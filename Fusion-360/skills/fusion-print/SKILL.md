---
name: fusion-print
description: Use the local Fusion Print CLI or MCP bridge to validate recipes, build new Fusion 360 parts, and inspect their exports. Use for Fusion Print recipe and bridge workflows; it does not provide generic existing-document editing or assembly inspection.
---

# Fusion Print

Use the installed local runtime, outside the management repository. Confirm its
root from local configuration. Locate the management checkout through the local project pointer or
3D_MODELING_HOME. Read its AGENTS.md and Fusion-360/AGENTS.md for modeling
rules, Fusion-360/runtime-scope.md for supported CAD scope, and
connections.md when setting up or relocating the bridge.

## Choose the operation

- Before live work, run `fusion-print doctor` and then `fusion-print ping`.
  A heartbeat alone does not prove the Fusion main thread is responsive.
- A model argument is relative to the runtime's `models/` directory:
  `fusion-print validate <part>/model.json`.
- Use `build <part>/model.json --wait 30` only when creating a new document is
  consistent with the user's request. The CLI does not edit an existing document.
- Record the returned job ID. After a timeout, query `status <ID> --wait 30`;
  do not submit another build while the original outcome is unknown.
- Use `inspect-mesh <ID>` on existing exports. It does not query live CAD or
  certify slicer/CAM readiness.

Run from the runtime root, or pass `--root <local-runtime-root>` before the command.
MCP equivalents are `fusion_health`, `fusion_ping`, `fusion_validate`,
`fusion_build`, `fusion_job_status`, and `fusion_inspect_mesh`; verify their
installed schemas. MCP build returns an ID immediately.

## Recipes and evidence

Before writing or changing a recipe, read [recipe contract](references/recipe-contract.md).
Store model.json, recipe.py and reference images in the private local workspace.
Do not read old task folders merely because they exist.

Inspect the final job's CAD report, mesh report and images. A failed or missing
export is incomplete work. Reuse read-only inspection/export tools where available;
do not rebuild a model merely to check it. A user-edited CAD document may differ
from its source recipe; record that difference before regenerating.
