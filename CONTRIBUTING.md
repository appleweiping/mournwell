# Contributing to MOURNWELL

Thanks for helping improve the well. Keep contributions original: do not submit
copyrighted game assets, extracted audio, copied level data, or trademarks from
another title.

## Local setup

```bash
git clone https://github.com/appleweiping/mournwell.git
cd mournwell
npm ci
npx playwright install chromium
npm run test:all
```

Node.js 22 or newer and npm 11.17.x are required. npm 11 enforces the exact
install-script allowlist in `package.json`; older npm versions are unsupported.
The project intentionally has no secrets or runtime environment file.

## Change workflow

1. Create a focused branch from the current `main`.
2. Add or update tests for behavior changes. Seeded fixtures are preferred over
   timing-dependent setup.
3. Run `npm run test:all` and `npm run audit:prod`.
4. Update documentation and deterministic demo captures when UI or flow changes.
5. Open a pull request that explains intent, risk, test evidence, and any
   player-facing change.

Do not commit `dist`, Playwright reports, dependency folders, generated traces,
or local editor settings. Use `npm run format:write` before submitting.

## Engineering conventions

- Pure deterministic rules belong in `src/game/systems` or `src/game/data` and
  should be unit tested without Phaser.
- Rendering, physics, and lifecycle integration belong in scene/entity adapters.
- Never use `Math.random()` for authored run state; request a named seeded RNG
  stream so the same seed stays reproducible.
- Keep the production debug bridge read-only. New QA commands must remain gated
  behind `import.meta.env.DEV && ?qa=1`.
- Touch interactions must preserve independent pointer ownership and handle
  `pointerup`, cancellation, and lost pointers.
- Maintain keyboard focus visibility, sufficient contrast, and readable labels.

## Bug reports

Include the seed shown in the result screen, browser/device, exact input steps,
expected behavior, actual behavior, and a screenshot or trace when possible.
Report security concerns privately as described in [SECURITY.md](./SECURITY.md).
