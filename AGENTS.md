# Repository Guidelines

## Project Structure & Module Organization
- `index.html`는 허브 랜딩 페이지입니다. 신규 섹션이나 링크를 추가할 때는 시각적 일관성과 최소 JS 원칙을 유지하세요.
- `routine/` 폴더에 타이머 앱이 있으며, 스크립트는 ES 모듈로 유지하고 추가 의존성은 CDN으로 명시적으로 불러오세요.
- `저속노화.html`은 Tailwind 기반의 단일 HTML 페이지입니다. 문서 개편 시 Tailwind CDN 설정을 재사용하고 불필요한 JS 추가를 피하세요.
- `README.md`는 기능 사용법과 Supabase 설정을 문서화합니다. 플로우 변경 시 즉시 업데이트하세요.
- 신규 정적 자산은 루트에 두고 상대 경로로 참조하면 GitHub Pages 배포가 용이합니다.

## Build, Test, and Development Commands
- `python -m http.server 8000`를 루트에서 실행하면 전체 페이지를 미리볼 수 있습니다. 허브는 `/index.html`, 타이머는 `/routine/` 경로로 접근하세요.
- `open routine.html` (macOS) 또는 `xdg-open routine.html`로 Supabase 연동 없이도 타이머 UI를 빠르게 검증할 수 있습니다.
- Supabase 퍼시스턴스 검증 전에는 `README.md`의 SQL을 적용하고 anon 키를 타이머 설정 패널에 입력하세요.

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
