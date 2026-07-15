# dimos-docs-assets

Binary media (screenshots, plots, diagrams, video stills) displayed by the
[dimos](https://github.com/dimensionalOS/dimos) documentation site.

These files live here as plain git blobs instead of inside `dimos` because:

- Mintlify (which deploys the docs site) does not fetch Git LFS objects, so
  LFS-tracked images render as broken pointer text on the published site.
- Committing binaries directly to `dimos` bloats every checkout, and the
  `largefiles_check` pre-commit hook there rejects non-LFS files over 75 KB.
- `raw.githubusercontent.com` serves plain blobs CDN-cached with no LFS
  bandwidth quota.

## Layout

Paths mirror the `docs/` tree in `dimos`, minus the `docs/` prefix:

```
dimos:  docs/capabilities/navigation/assets/coverage.png
here:   capabilities/navigation/assets/coverage.png
```

## Linking from docs

Reference assets with an absolute URL pinned to `main`:

```markdown
![Coverage](https://raw.githubusercontent.com/dimensionalOS/dimos-docs-assets/main/capabilities/navigation/assets/coverage.png)
```

These URLs render both on GitHub and on the Mintlify site.

## Rules

- **Never move, rename, or delete a published file** — the docs URLs that
  point at it break silently. Add a new file instead and update the docs.
- **Updating an image in place is fine** (same path, new content) — the
  `main` URL picks it up; no docs change needed.
- **Workflow for new/changed images**: push the asset to this repo first,
  then open the dimos docs PR that references it.
- Regenerated diagram outputs (the `output=assets/...` code fences in dimos
  docs) are written locally by the docs tooling; upload the regenerated file
  here at the same path when a diagram changes.
