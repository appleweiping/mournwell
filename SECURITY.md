# Security policy

## Supported versions

Security fixes are applied to the latest release on `main`.

| Version | Supported |
| ------- | --------- |
| 1.x     | Yes       |
| < 1.0   | No        |

## Reporting a vulnerability

Please do not open a public issue for a suspected vulnerability. Use GitHub's
**Security → Report a vulnerability** flow for this repository so the report,
proof of concept, and discussion remain private.

Include the affected version or commit, browser and operating system, impact,
reproduction steps, and any suggested mitigation. Maintainers aim to
acknowledge a complete report within three business days, provide an initial
severity assessment within seven business days, and coordinate disclosure once
a fix is available. These are response targets, not a service-level agreement.

## Security posture

- The shipped game is a static client with no application server, account,
  cookies, analytics, advertising SDK, or gameplay-data transmission.
- Save data is schema-validated before use and remains in browser
  `localStorage` under `mournwell.save.v1`.
- QA mutation controls require both a development build and `?qa=1`; production
  builds expose only cloned read-only snapshots.
- CI runs strict type checking, lint rules including security checks, browser
  journeys, a production dependency audit, and CodeQL.
- Dependency updates are proposed automatically, but still require the full CI
  gate before merge.

If a future release introduces telemetry, authentication, payments, cloud
saves, user-generated content, or a backend, it requires a new threat model and
privacy review before deployment.
