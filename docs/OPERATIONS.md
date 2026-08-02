# Operations and release runbook

MOURNWELL is a static site. Its deployable artifact is `dist/`; runtime state is
limited to the current tab and the user's versioned local save.

Every build verifies that `dist/` carries the project license and complete
Phaser/EventEmitter3 MIT notices alongside the executable bundle.

## Build and deploy

```bash
npm ci
npm run test:all
npm run audit:prod
```

Merging to `main` runs CI and CodeQL. The Pages workflow builds the same static
artifact and deploys it only after its own clean install/build. `base: './'`
keeps asset URLs valid on GitHub Pages and other subpath hosts.

For another static host, publish the contents of `dist/` with HTTPS and a
fallback to `index.html` only if the host requires one. There are no server
routes, secrets, migrations, cron jobs, or runtime environment variables.

## Release checklist

1. Confirm `CHANGELOG.md`, version metadata, screenshots, and supported-browser
   notes match the candidate.
2. Run the clean release gate and visually inspect every deterministic capture.
3. Review dependency and CodeQL alerts; no unresolved high/critical issue is
   accepted.
4. Merge to `main`, wait for required checks, then create an immutable `vX.Y.Z`
   tag and GitHub release.
5. Smoke-test the deployed title, one combat room, touch controls at phone size,
   and the production `window.__game` read-only contract.

## Rollback

GitHub Pages artifacts are immutable per workflow run. Re-run the last known-good
tag/commit through the Pages workflow or revert the faulty commit and let CI
deploy the revert. Because there is no server data, schema migration, or remote
save, rollback cannot orphan backend state. Keep the local save schema backward
compatible; introduce a new storage key for a destructive future format change.

## Incident triage

Request the affected URL/commit, browser/device, seed, visible phase, console
output, and `window.__game.getSnapshot()` where safe. Reproduce with the seed in
a development `?qa=1` run. Classify:

- **Availability:** page or bundle does not load;
- **Integrity:** impossible dungeon, corrupt stats/save, or unrecoverable run;
- **Input:** keyboard/touch intent sticks, conflicts, or cannot reach an action;
- **Performance:** sustained frame loss or entity growth;
- **Security/privacy:** unexpected network activity, dependency compromise, or
  production mutation authority.

Security/privacy incidents follow `SECURITY.md` and should not be discussed in a
public issue before triage.

## Runtime diagnostics

The application intentionally sends no diagnostics off-device. During a support
session, the user can copy a snapshot locally:

```js
JSON.stringify(window.__game.getSnapshot(), null, 2);
```

The snapshot contains gameplay state and the user-chosen/generated seed, but no
account identifier because the product has no accounts. Browser developer tools
can confirm that a production session makes no gameplay API calls.

## Future commercial operations

Before adding monetization or distribution through a store, assign owners for
privacy, security response, legal/IP, release approval, customer support, device
certification, accessibility, localization, and business continuity. Define
measured SLOs only after hosting telemetry exists; this static open-source release
does not claim unmeasured uptime or performance guarantees.
