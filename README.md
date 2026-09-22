# Ember for Tabularis

[![Validate theme](https://github.com/TabularisDB/tabularis-ember-theme/actions/workflows/validate.yml/badge.svg)](https://github.com/TabularisDB/tabularis-ember-theme/actions/workflows/validate.yml)

A warm, two-variant theme for [Tabularis](https://tabularis.dev):

- **Ember Dark** — deep charcoal-brown surfaces with glowing amber accents.
- **Ember Light** — parchment surfaces with copper accents.

Both variants style the application, SQL editor and data grid with a coordinated semantic palette. Themes are declarative JSON, not executable plugins.

| Variant | Background | Text | Accent |
| --- | --- | --- | --- |
| Ember Dark | `#16110f` | `#f5ebe0` | `#f28c3c` |
| Ember Light | `#fbf5ec` | `#2b2018` | `#c9631f` |

## Compatibility

Requires Tabularis **0.25.1-1 or later**: the nightly that first accepts a manifest
with a stable package `id` and a free-form display `name`, following the current
Tabularium manifest schema. Any later nightly and the next stable release (0.25.1 or
newer) also work. Tabularis 0.25.0 rejects this package, because its bundled schema
predates the `id` field.

## Installation

1. Download `theme-universal.zip` from this repository's GitHub Releases.
2. In Tabularis, open **Settings → Appearance → Manage themes → Local package**.
3. Preview and install the package.
4. Select **Ember Dark** or **Ember Light** and apply it. Installation alone does not change the selected theme.

The ZIP is universal: the same file works on all supported operating systems.

## Editing and validation

Edit `themes/dark.json` and `themes/light.json`. Application colors live under
`colors`; Monaco colors and SQL token rules remain under `editor`.

The `$schema` hints let external editors offer completion and validation. The
manifest uses Tabularium's schema; theme definitions use the canonical schema on GitHub:

| File | Public schema |
| --- | --- |
| `.tabularium` | https://registry.tabularis.dev/manifest.schema.json?kind=theme |
| `themes/*.json` | https://raw.githubusercontent.com/TabularisDB/tabularis/main/src/schemas/theme-definition-v1.json |

To check the manifest against the live registry schema and build the package
locally, with Node.js 22 and no account or token:

```sh
npx --yes @tabularium/cli validate .tabularium --registry https://registry.tabularis.dev --kind theme
zip -X -D -r theme-universal.zip .tabularium LICENSE.txt README.md themes
```

Validation does not submit or publish the theme.

## CI and releases

- **Branch pushes / pull requests:** validate the manifest against the live
  Tabularium schema and build the ZIP. The workflow has read-only permissions
  and needs no secrets.
- **Version tags:** check that the tag matches the manifest version, validate,
  build, then create a **draft** GitHub release containing `theme-universal.zip`.

Releasing a version:

1. Increment `version` in `.tabularium`. If the theme starts relying on newer host
   features, raise `min_runtime_version` to the first Tabularis release providing them.
2. Tag and push:

   ```sh
   git tag v1.0.0
   git push origin v1.0.0
   ```

3. Review the generated draft and ZIP, then publish the release.
4. Submit this repository through Tabularium. Registry approval and ingestion are
   separate from GitHub release publication.

Keep the package `id` and variant IDs stable across versions.

## License

Theme palettes: **MIT**, copyright Andrea Debernardi; see [LICENSE.txt](LICENSE.txt).

[Theme authoring guide](https://github.com/TabularisDB/tabularis/blob/main/packages/create-plugin/THEMES.md)
