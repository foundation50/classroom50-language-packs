# classroom50-language-packs

Community and machine-generated **language packs** for
[Classroom 50](https://github.com/foundation50/classroom50) — a self-hosted
GitHub Classroom. Each `<code>.json` is a translation of the app's base locale
(`en.json`), installable at runtime with no rebuild.

## How packs are produced

A CI pipeline in the `classroom50` repo regenerates each target language from
`en.json` with AWS Bedrock and opens a **pull request per language** here. The
translations reuse the app's translation prompt and are structurally validated
(key/placeholder parity) before the PR is opened. A human reviews the diff and
merges to publish — so every published string has been eyeballed at least once.

Because packs are regenerated from the current `en.json` on each run and read
the published file back as their baseline, **hand edits are safe**: correct a
string in a merged pack and the next run preserves it, only re-touching values
whose English changed.

## Installing

Packs are served publicly via GitHub Pages:

- `https://foundation50.github.io/classroom50-language-packs/<code>.json` — a pack
- `https://foundation50.github.io/classroom50-language-packs/index.json` — the manifest of published codes

In the app: account menu (avatar) → **Language** → paste a pack URL, or upload
the downloaded `.json`. See the
[language pack guide](https://github.com/foundation50/classroom50/blob/main/web/src/locales/README.md)
for the full contract (validation rules, partial-pack fallback, placeholders).

## Contributing a correction

Open a PR editing the relevant `<code>.json` (keep every key and every
`{{placeholder}}` intact — translate only the values). On merge, GitHub Pages
redeploys and the CI pipeline preserves your correction going forward. See
[CONTRIBUTING.md](CONTRIBUTING.md) for the full contract and workflow.

## Publishing (maintainers)

`.github/workflows/publish-pages.yaml` deploys the merged packs on `main` to
GitHub Pages on every push touching a `*.json` file. One-time setup:
**Settings → Pages → Source = GitHub Actions**.
