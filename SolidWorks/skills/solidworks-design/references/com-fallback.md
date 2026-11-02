# SolidWorks COM fallback

Use only when SolidWorks MCP is unavailable or a real MCP call failed. Report the
actual access method and failure without putting private logs in a public repository.

- Connect to the intended existing session; do not silently replace a document.
  Inspect the target read-only before changing it.
- Keep temporary helpers, binaries, logs, and measurements in the private task
  workspace. Prefer native features and preserve editable source geometry.
- Validate the saved document with a separate readback. Use MCP if it becomes
  available; otherwise report COM readback, rebuild errors/warnings, dirty state,
  active configuration, and any unverifiable checks.
- After two focused signature attempts fail, inspect installed API documentation
  or choose a documented alternative; do not keep guessing numeric arguments.
- Dimension creation may open a blocking Modify dialog. If unattended construction
  needs `swInputDimValOnCreate` disabled, record and restore it in `finally`.
  Resolve constants from the installed type library or authoritative documentation.
- A generated-wrapper failure does not itself prove the application is disconnected.
  Check an existing-session dynamic dispatch connection before diagnosing connectivity.
- A no-argument getter can appear as a value or bound method. Inspect the returned
  object before invoking it; COM objects can themselves have callable default members.
- Output-parameter conventions differ between wrappers. Inspect the installed
  signature and test one read-only call before assuming BYREF or tuple behavior.
- If computer control is requested back, stop mouse/keyboard automation immediately.
  Use compatible nonmodal background calls only; never dismiss unknown dialogs blindly.

For deterministic insertion and inference settings, read
[parametric sketches](parametric-sketches.md).
