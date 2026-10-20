# Contributing to Kacky Live

Thanks for helping build Kacky Live! To keep reviews fast and painless, we aim for small, focused pull requests tied to open issues.

By participating, you agree to follow our [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

## Workflow

1. **Pick an issue:** Browse open issues or open a new one to discuss a change before writing a lot of code.
2. **Branch off `main`:** Create a feature branch on your fork (one pull request per issue).
3. **Keep PRs small:** Aim for under ~400 changed lines so reviews stay quick.
4. **Check before adding dependencies:** Comment in the issue before introducing a new npm package.
5. **Include visuals:** If your PR changes the UI, include a `1920x1080` screenshot in the PR description.

## Architecture & Overlay Rules

Before writing code, check [`docs/API-NOTES.md`](docs/API-NOTES.md) for endpoint details.

- **Read-only public API:** We only use anonymous `GET` requests against the documented KackyGG `/v1` endpoints. No auth, cookies, scraping, or custom backend endpoints.
- **No secrets in the repo:** Never commit tokens, private server logins, or `.env` files.
- **Strip Trackmania formatting:** Always strip Trackmania colour and style codes (`$f00`, `$i`, `$o`, `$w`, etc.) before rendering player or map names.
- **Keep the overlay quiet:** Streamers are trying to land frame-perfect tricks. Avoid flashy animations or popups that pull attention away from the car.
- **Test behaviour changes:** Add or update unit tests when changing data parsing, polling, or state logic.

## Reviews

All pull requests are reviewed and merged by the maintainers:

- [@Thorbenl](https://github.com/Thorbenl)
- [@bompi-me](https://github.com/bompi-me)
