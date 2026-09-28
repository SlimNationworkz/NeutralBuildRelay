# Slim Nation Works Neutral Build Relay

Public relay repository: `SlimNationworkz/NeutralBuildRelay`

Git identity:
- Name: `SlimNationworkz`
- Email: `slimnationworkz@gmail.com`

## Purpose

Build a temporary **debug APK** from an exact approved commit in one of two
private source repositories without moving source code into the public relay:

- `breakwave` -> `lindsey-wells/breakwave`
- `scratchless` -> `cube23games/Scratchless`

The private repository stays private. Only the resulting APK plus a checksum
manifest are published.

## Trust boundary

This relay is intentionally NOT authoritative CI and never promotes source.

The private source project's own gates remain authoritative. The relay:

1. accepts only `breakwave` or `scratchless`
2. requires an exact 40-character commit SHA
3. checks out with a **read-only deploy key**
4. verifies checkout HEAD equals the requested SHA
5. builds a debug APK with output redirected away from public logs
6. uploads only `relay_output/**`
7. publishes a temporary prerelease only in a separate job that has no private
   source deploy key
8. automatically removes relay prereleases after 24 hours

## Public workflow safety

`workflow_dispatch` is the only build trigger. GitHub requires write access to
manually dispatch it.

Do NOT add `pull_request_target`, arbitrary repository inputs, arbitrary shell
inputs, or source upload steps.

Treat changes under `.github/workflows/` as security-sensitive.

## Why debug APK

The relay is for QA/temporary distribution. Debug builds avoid putting a
production Android signing key into a public relay repository.

## Required secrets

In `SlimNationworkz/NeutralBuildRelay`:

- `BREAKWAVE_DEPLOY_KEY`
- `SCRATCHLESS_DEPLOY_KEY`

Each is a unique SSH private key. Its corresponding public key is installed as
a **read-only deploy key** on exactly one private source repository.

## BreakWave current test dispatch

- project: `breakwave`
- source_sha: `3c740f28ca096c7b286a9886d9ef4451eb375187`
- flutter_version: `3.44.9`
- delivery: `public-release`

This does not alter BreakWave `main`, tags, branches, releases, or Actions
artifacts.
