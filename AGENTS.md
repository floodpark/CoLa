# Repository Guidelines

## Project Structure & Module Organization
- `index.html` hosts the entire app, including markup, scoped CSS inside `<style>`, and an ES module script; keep new logic within the module or import additional CDN modules explicitly.
- `README.md` documents usage and Supabase setup—update it whenever user flows or environment steps change.
- `저속노화.md` stores auxiliary notes; keep supplementary documentation or Korean copy edits there to avoid cluttering the main guide.
- Place any new static assets alongside `index.html` and reference them with relative paths so GitHub Pages can serve them without extra configuration.

## Build, Test, and Development Commands
- `python -m http.server 8000` from the repo root serves the app locally; visit `http://localhost:8000/index.html` for manual QA.
- `open index.html` (macOS) or `xdg-open index.html` offers a quick, serverless preview when Supabase integration is not required.
- Apply the Supabase SQL in `README.md` before validating persistence; supply the anon key via the settings panel to populate `localStorage`.

## Coding Style & Naming Conventions
- Use 4-space indentation across HTML, CSS, and JavaScript; wrap attributes or long declarations onto new lines when they exceed roughly 100 characters.
- Favor `const`/`let` with camelCase identifiers (`saveSupabaseSettings`, `setDurationSeconds`); reserve PascalCase for future classes or components.
- Keep CSS selectors descriptive (`.status-pill`, `.app-card`) and group related declarations together; expand `:root` custom properties thoughtfully instead of adding scattered inline styles.

## Testing Guidelines
- Perform manual flows: load the page, configure a short routine (e.g., 1 set × 10 seconds), and observe timer transitions, pause/resume behaviour, and log entries.
- Verify Supabase writes through DevTools → Network; confirm the `insert` call resolves without errors and repeat after clearing settings to ensure graceful handling.
- Document browser quirks or timing adjustments in `README.md` until an automated harness is introduced.

## Commit & Pull Request Guidelines
- Follow concise, imperative commit subjects similar to `Create index.html`; lead with scope (`Timer:`) when multiple areas change and elaborate in the body if needed.
- Reference related GitHub issues and summarise test coverage in each PR; attach screenshots or GIFs for UI-affecting updates.
- Call out Supabase schema or RLS changes explicitly and include SQL snippets or migration steps in the PR description.

## Supabase & Security Notes
- Commit only anon keys; never expose service role, JWT secrets, or `.env` files in the repository.
- Keep payload keys (`set_count`, `completed_sets`, etc.) aligned with the production table schema and update policies before merging breaking changes.
- Rotate anon keys and update the README if credentials appear in history; treat Supabase project configuration changes as part of release notes.
