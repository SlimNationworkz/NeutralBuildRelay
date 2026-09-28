# Relay Security Rules

1. Public relay repo: `SlimNationworkz/NeutralBuildRelay`.
2. Private sources remain private.
3. One unique read-only SSH deploy key per source repository.
4. Never reuse the BreakWave deploy key for ScratchLess or vice versa.
5. Build trigger stays `workflow_dispatch` only.
6. Never use `pull_request_target`.
7. Never accept arbitrary repository URLs, branches, scripts, or commands.
8. Exact 40-character source SHA is mandatory.
9. Build job gets only `contents: read` on the public relay.
10. Publish job gets `contents: write` but receives no private source key.
11. Only APK + checksum/manifest are uploaded.
12. Private checkout tree and private build logs are never uploaded.
13. Relay APK is debug/QA only, not a production signing path.
14. Relay release cleanup removes `relay-*` prereleases older than 24 hours.
15. Source-project promotion remains a separate human-approved process.
