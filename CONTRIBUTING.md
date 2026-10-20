# Contributing to Kacky Live

Thanks for helping build Kacky Live! To keep reviews fast and painless, we aim for small, focused pull requests tied to open issues.

By participating, you agree to follow our [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

## Workflow

1. **Pick an issue:** Browse open issues or open a new one to discuss a change before writing code.
2. **Branch off `main`:** Create a feature branch on your fork (one pull request per issue).
3. **Keep PRs small:** Aim for under ~400 changed lines so reviews stay fast.
4. **Check before adding dependencies:** Comment on the issue before introducing new npm packages.
5. **Include visuals:** If your PR changes UI, include a screenshot or short clip in the PR description.

## Development Guidelines

Check [`docs/API-NOTES.md`](docs/API-NOTES.md) for endpoint schemas and polling intervals.

- **Public API only:** The overlay runs client-side using documented KackyGG `/v1` endpoints without authentication.
- **Clean names:** Always strip Trackmania color and style codes (`$f00`, `$i`, `$o`, `$w`, etc.) before rendering player nicknames or map titles.
- **Stream-safe visuals:** Keep animations subtle. The game screen is fast and intense; the overlay shouldn't distract from the car.
- **Tests:** Add or update tests when touching data mappers, polling hooks, or fallback states.

## Reviews

All pull requests are reviewed and merged by the maintainers:

- [@Thorbenl](https://github.com/Thorbenl)
- [@bompi-me](https://github.com/bompi-me)
