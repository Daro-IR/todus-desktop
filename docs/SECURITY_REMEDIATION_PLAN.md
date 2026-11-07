# Security remediation plan — toDus Desktop

> Status: planning branch only. This document does not claim that any vulnerability has been fixed.
> Scope: static review of repository content available during the 2026-11-07 review. The current `main` branch contains only the README; the application source reviewed earlier is available only in historical Git objects. Re-run every check against the exact source used to build the current release before shipping changes.

## Release gate

- [ ] Recover the authoritative source for the released application from a trusted local backup or build workspace.
- [ ] Verify that the recovered source corresponds to the published 1.0.1 installer (record commit, build environment, dependency lockfile and artifact hashes).
- [ ] Do not merge security fixes or publish a replacement installer until the source-to-binary relationship is established and regression tests pass.

## Priority 0 — exposed credentials and historical data

- [ ] Treat any static TURN credential found in historical client code as compromised. If the service is controlled by the project maintainer, rotate/revoke it; otherwise notify the service owner. Do not place replacement credentials in client-side code.
- [ ] Review historical Git objects for personal data and credentials. Remove sensitive material from reachable history where possible and request GitHub Support assistance for cached/unreachable objects when necessary.
- [ ] If any exposed phone numbers or account identifiers belong to active test accounts, disable or change those accounts' credentials.
- [ ] Scan all branches, tags, releases, workflow logs and build artifacts for secrets before the next release.

## Priority 1 — local credential storage

- [ ] Replace plaintext storage of authentication passwords/session tokens with Windows DPAPI or Windows Credential Manager.
- [ ] Keep the renderer-facing IPC surface minimal; never return passwords, refresh tokens or complete authentication objects to the renderer unless strictly required.
- [ ] Add explicit logout/session revocation and safe migration from legacy local storage.
- [ ] Ensure logs, crash reports and diagnostics redact credentials and personal identifiers.

## Priority 1 — auxiliary HTTP server

- [ ] Confirm whether the auxiliary web server is used in production. If not required, remove it from production packaging/start scripts.
- [ ] If retained, bind only to loopback by default.
- [ ] Resolve requested paths against a fixed document root, normalize them, and reject any path that escapes that root.
- [ ] Serve only an explicit allowlist of files; reject traversal encodings and unexpected methods.
- [ ] Add automated tests for traversal attempts, encoded paths, symlinks and access from non-loopback interfaces.

## Priority 1 — WebRTC/TURN configuration

- [ ] Remove static TURN usernames/passwords from shipped HTML/JavaScript.
- [ ] Use short-lived TURN credentials issued by a trusted backend, or document and validate the intended public relay configuration.
- [ ] Verify transport security and restrict relay usage/rates where the service supports it.

## Priority 2 — release and update integrity

- [ ] Verify updater manifest signatures or use a signed, authenticated update mechanism; do not rely on transport alone as the trust boundary.
- [ ] Validate downloaded installer hashes against a trusted release manifest and reject unexpected downgrade or version rollback.
- [ ] Test update, interrupted download, corrupt package, rollback and offline behavior on clean Windows test machines.
- [ ] Preserve build provenance: source commit, dependency lockfile, toolchain versions and artifact SHA-256.

## Verification checklist

- [ ] Static secret scan across the complete source history and release artifacts.
- [ ] Dependency audit against the exact lockfile used for the release.
- [ ] IPC authorization and input-validation review.
- [ ] Local storage inspection on a disposable Windows test profile.
- [ ] HTTP server path traversal and network-binding tests, if that component remains.
- [ ] Updater integrity and rollback tests.
- [ ] Regression tests for login, messaging, groups, drafts, session migration and storage-directory selection.

## Important limitations

This plan is not a penetration-test certificate. The released Windows installer was not unpacked or executed during the review, and no production service was probed. Findings from historical source must be revalidated against the source that produced the current installer before being treated as current-release defects.
