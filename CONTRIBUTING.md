# Contributing to classroom50-language-packs

Thanks for helping improve the translations for
[Classroom 50](https://github.com/foundation50/classroom50), the open-source
[GitHub Classroom](https://classroom.github.com/) alternative supported by the
[Fifty Foundation](https://fifty.foundation/).

This repo holds the **language packs** — one `<code>.json` per locale (a
translation of the app's base locale,
[`en.json`](https://github.com/foundation50/classroom50/blob/main/web/src/locales/en.json)).
Most contributions here are small: fixing an awkward phrase, a typo, or a term
that reads wrong in your language. Those are exactly the changes we want.

New here? See the [README](README.md) for how packs are produced, installed,
and published. This guide covers how to *contribute a change*.

## Ways to contribute

- **Fix or improve a translation** — open a pull request editing the relevant
  `<code>.json` (see below).
- **Report a bad string** without fixing it — open an
  [issue](https://github.com/foundation50/classroom50-language-packs/issues/new)
  with the locale, the key, and what's wrong.
- **Request a new language** — open an issue. New languages are added on the
  `classroom50` side (its `targets.json`), then generated and opened here as a
  PR; you don't need to hand-write a new pack from scratch.

Please keep tokens, secrets, and private student data out of issues and PRs.

## The one rule: translate values, keep structure

Every pack must stay **structurally identical** to `en.json` — same keys, same
nesting, same `{{placeholders}}`. The app and the CI both reject packs that
drift. So when you edit a `<code>.json`:

- **Only change the string values.** Never rename, add, remove, or reorder
  keys.
- **Keep every `{{placeholder}}` intact**, spelled exactly as in the English
  source (e.g. `{{count}}`, `{{name}}`). You may move a placeholder within the
  sentence to fit your language's word order, but don't rename it, drop it, or
  invent new ones.
- **Leave values as strings.** No numbers, booleans, or nested objects on a
  leaf.
- **Don't translate the keys or `en.json`** — the
  [English file](https://github.com/foundation50/classroom50/blob/main/web/src/locales/en.json)
  is the source of truth and lives in the `classroom50` repo, not here.

Plural forms are the one place extra keys are allowed: i18next plural variants
(`_zero`, `_one`, `_two`, `_few`, `_many`, `_other`) of a key that already has a
`_one`/`_other` in the base are accepted, so you can add the plural categories
your language needs.

## Making a change

1. **Fork** this repo and create a branch.
2. Edit the `<code>.json` for your locale (e.g. `fr.json`, `pt-BR.json`).
   Change only values, per the rule above.
3. **Validate locally** (optional but encouraged) — the same check CI uses:

   ```sh
   # from a clone of the classroom50 repo, in web/src/locales,
   # with your edited pack copied in as <code>.json:
   python verify_locale.py fr.json
   ```

   It prints `PASS`/`FAIL` and lists any missing/extra keys, non-string values,
   or placeholder mismatches. `verify_locale.py` lives in
   [`web/src/locales/`](https://github.com/foundation50/classroom50/blob/main/web/src/locales/verify_locale.py)
   of the `classroom50` repo.
4. **Open a pull request** against `main`. A maintainer reviews the diff and
   merges (squash). On merge, GitHub Pages redeploys and your change goes live
   at `https://foundation50.github.io/classroom50-language-packs/<code>.json`.

## Your edits are safe across regenerations

Packs are periodically regenerated from the latest `en.json` by CI. This does
**not** clobber your work: the pipeline re-translates only the keys whose
*English* changed since the pack was last built, and carries every other
value — including your corrections — through untouched. So a merged fix
survives future runs unless the English for that exact string changes.

## Commits and pull requests

We squash-merge, so the **PR title becomes the commit** on `main`. Use a short,
imperative summary; the [Conventional Commits](https://www.conventionalcommits.org/)
style used across Classroom 50 is welcome but not required for translation
edits. Examples:

- `fix(fr): correct wording of the assignment accept button`
- `docs: clarify placeholder rule`

Keep PRs focused — one locale (or one theme) per PR makes review quick.

## License

By contributing, you agree that your contributions will be licensed under the
[GNU General Public License v3.0](https://github.com/foundation50/classroom50/blob/main/LICENSE),
matching the Classroom 50 project.
