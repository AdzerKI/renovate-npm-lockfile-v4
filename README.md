# renovate-npm-lockfile-v4

Minimal reproduction: Renovate can't read a `package-lock.json` with `lockfileVersion: 4`.

npm 12 writes lockfile version 4 as soon as `patchedDependencies` (or `packageExtensions`) is used. This repo was created with npm 12.2.0: `npm install`, then `npm patch add has-flag` / `npm patch commit`.

Run:

```sh
LOG_LEVEL=debug renovate --platform=local --dry-run=lookup
```

Renovate logs `Npm: unable to parse lockfile` and `WARN: Found unsupported npm lockfile version`, no dependency gets a `lockedVersion`, and no npm constraint is derived from the lockfile.
