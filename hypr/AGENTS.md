# Repository Guidelines

## Project Structure & Module Organization
Hyprland reads `hyprland.conf` first, then layers the repo defaults from `~/.local/share/omarchy/default/hypr/*.conf` before applying the overrides in this directory. Touch only the files under `~/.config/hypr/` when adjusting the active configuration. Use `monitors.conf` for display geometry, `input.conf` for keyboards and pointers, `bindings.conf` for keymaps, `envs.conf` for session-wide variables, `looknfeel.conf` for appearance tweaks, and `autostart.conf` for background services. Keep any experimental rules at the bottom of `hyprland.conf` so they are easy to audit.

## Build, Test, and Development Commands
Reload changes in place with `hyprctl reload`; prefer that over restarting the compositor. Validate monitors or inputs before committing by running `hyprctl monitors`, `hyprctl devices`, and `hyprctl configerrors` to catch typos. When iterating on scripts referenced from `autostart.conf`, launch them manually with `hyprctl dispatch exec "[command]"` to confirm they behave under Hyprland.

## Coding Style & Naming Conventions
Configurations use two-space indentation and align on `key = value` pairs, as the existing files do. Comment rationale with `#` above the lines they explain and avoid in-line trailing notes that can break parsing. Order environment exports (`env =`) and bindings (`bind =`) by scope: global first, then workspace-specific tweaks. Mirror Hyprland’s canonical names—e.g., `monitor`, `env`, `bindm`—and keep custom script paths under `~/.local/bin/` with descriptive snake_case filenames.

## Testing Guidelines
Before pushing changes, run `hyprctl reload` and check `~/.local/state/hypr/Hyprland/errors.log` for warnings. For monitor or scaling edits, temporarily disconnect/reconnect displays after reloading to ensure the compositor applies the new layout. Document non-obvious behaviors (like NVIDIA-specific `env =` entries) directly in the relevant file so other agents understand the constraint.

## Commit & Pull Request Guidelines
Use imperative commit subjects (`Adjust monitor scaling`, `Add clipboard binding`) and group related config edits together. Reference downstream issues or tasks in the body and list the touched files for quick review. Pull requests should summarize visible effects, mention any scripts or services that require manual installation, and include screenshots or command output when layout or visual changes are involved. Always note follow-up work if a change introduces temporary workarounds.
