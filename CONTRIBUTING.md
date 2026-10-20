# Contributing

Kacky Live is an open source project. Keep changes small and easy to review.

By participating, you agree to follow the [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

## Workflow

- Work on a branch. Never push to `main`.
- Open one pull request per issue.
- Link the issue in the pull request body.
- Keep the pull request under about 400 changed lines. Split larger work.
- Ask in the issue before adding a dependency.
- Pull requests need one approving review from a maintainer.

## Rules

- Read `README.md` and `docs/API-NOTES.md` before you start.
- Public `GET` endpoints only. No writes, no auth, no cookies.
- No secrets in the repository or the client bundle.
- No new backend endpoints. If one is missing, write the case in the issue and wait.
- No scraping. Use the documented API.
- No changes to `kacky-ds` or the main website.
- Behaviour changes start with a failing test.
- Strip Trackmania colour codes before rendering a name.
- Keep the overlay quiet. No animation that pulls attention from the game.

## Review

- A maintainer reviews every pull request.
- A pull request needs one approval before it merges.
- A visual change needs a screenshot at 1920x1080 in the pull request.
- Only maintainers merge to `main`.

## Maintainers

- [@Thorbenl](https://github.com/Thorbenl)
- [@bompi-me](https://github.com/bompi-me)

## Writing

- Plain English, active voice.
- No em dashes in code comments, commit messages or pull request bodies.
- Short commit messages that say what changed.
