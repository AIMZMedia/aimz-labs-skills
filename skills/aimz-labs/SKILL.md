---
name: aimz-labs
description: Use AIMZ LABS through its connected MCP server to create and inspect media, run Labs workflows and workspace nodes, or build, edit and capture 3D blockout scenes. Use for AIMZ LABS requests, not unrelated ComfyUI administration.
---

# AIMZ LABS MCP

## Connect and discover

- Use the connected AIMZ LABS MCP server and read its initialization instructions and tool schemas. Discover the currently available tools; the server and documentation can change. Start with `whoami` when account context matters. See https://aimzlabs.com/docs/mcp and https://aimzlabs.com/docs/mcp/tools.
- The skill does not install or connect the MCP server. If it is missing, direct the user to the setup guide: install the AIMZ CLI, run `aimz login` themselves, and use `aimz mcp-config` to configure their client. Never ask the user to paste passwords, credentials or login tokens into chat.
- Respect the configured credit approval policy and the server's confirmation flow. Explain estimates before billed work, follow actual user confirmation and never invent confirmation tokens or silently change approval mode. Preserve existing user data and avoid unnecessary deletion.

## Generation and workflows

- Inspect models and inputs before submitting generation. Use estimates where available, then follow the returned job state. A timeout does not mean a job was not submitted; check the existing job before retrying to avoid duplicate cost.
- Labs workflows: discover with `list_workflows` and `get_workflow`, estimate with `workflow_estimate`, and start with `workflow_start`. Use a fresh run ID matching `r_[a-z0-9]{4,38}` for each new run. Call `workflow_plan`, then `workflow_step` with its returned `plan_hash`; if a step is still pending, wait on the same run and plan rather than starting another run.
- Workspace: use `workspace_list`, `workspace_get`, and `workspace_plan` before `workspace_generate`. Give each new request a unique 8–40 character ASCII letter, digit, underscore or hyphen `request_id`; reuse it while waiting on that request. Once complete, `workspace_copy_result` saves into a new copy using the returned `updated_at` as `expected_updated_at`.
- Labs workflows, workspace nodes and ComfyUI Hub are distinct. Automatic whole-workspace chains and YouTube source nodes are not covered by these tools. Check live schemas and report unsupported steps rather than claiming they ran.

## 3D blockout and video

- Call `scene_catalog` for current shapes and operations. Use `scene_create` for a new scene or `scene_get` and `scene_apply` to modify a saved scene. Build with named primitives via `add_prop`; use `edit_prop` for a part's shape, color or visibility and `transform` for its position, rotation or scale. Add and animate cameras using the catalog's operations.
- Review each operation's result. If a batch partially succeeds, retry only the unsuccessful operations after inspecting the scene. On a revision conflict, fetch the latest scene and reconcile changes before retrying. Do not overwrite someone else's work.
- Use `scene_inspect` to check camera framing and `scene_capture` with `kind="image"` or `kind="video"` to save a local preview. Capture needs a supported browser and Playwright; scenes referencing local models not uploaded to the service may not render in a fresh browser. Confirm the produced file and path. Primitive composition does not provide vertex editing or boolean modeling.
- A captured preview is distinct from billed AI video generation. If the user wants AI generation from the capture, inspect the selected model's actual input schema and file requirements, estimate its cost, and obtain any required approval first.
