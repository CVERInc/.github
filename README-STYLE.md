# CVER README house style

The contract for every public `CVERInc` repository README. Adopted 2026-06-10.

## Language policy

1. **`README.md` is English, always.** No parallel translated sections, no
   `README.<locale>.md` translation files. GitHub's audience is developers,
   and the portfolio's localization layer is the website.
2. **cver.net is the only multilingual surface.** Each product's localized
   intro lives at `cver.net/<locale>/oss/<repo>` (en-US / ja-JP / zh-TW).
   Deep operational guides for non-developer audiences belong in the product
   itself (e.g. seikyusho generates its Japanese 使い方 sheet inside the
   copied spreadsheet), never in the repo.
3. **Pointer line.** When localized detail pages exist, link them right
   below the badges, each locale in its own language with a per-locale
   deep link:

   ```
   🌐 日本語の紹介 → [cver.net/ja-jp/oss/<repo>](…) ・ 繁體中文介紹 → [cver.net/zh-tw/oss/<repo>](…)
   ```

4. Product-internal strings (menu names like 請求書, sheet tabs like 設定,
   button labels) stay verbatim in whatever language the product ships them —
   they are identifiers, not prose. Same for the repo *description* field,
   which may carry non-English keywords for GitHub search discovery.

## Skeleton

In order, top to bottom:

1. `# <lowercase repo name>` — the name is the H1, nothing else.
2. Blockquote **bold-led tagline** — verb-first, one or two sentences.
   A name gloss is welcome (e.g. *seikyusho（請求書）is Japanese for "invoice."*).
3. Badges (License first).
4. Pointer line to localized pages (if detail pages exist).
5. `---`
6. Body sections as `##`, in roughly this order, keeping only what applies:
   `What & why` · `Features` · `Install` / `Quick start` · `Usage` ·
   `How it works` · `Configuration` · `FAQ` · `Development` ·
   `Contributing` · `License`.

No emoji prefixes in headings. `<details>` blocks are fine for long
optional paths (alternative install methods, FAQ entries).

## Voice

- Taglines are verb-first and concrete: *"Sift the near-duplicate snaps…"*,
  *"Tug tiles to plan…"*, *"Bind the paper you already own…"*.
- Ownership framing (*the X you already own*, *no upload, no server, yours*)
  is a recurring portfolio signature — use it where true.
- State non-goals and boundaries explicitly; restraint is a feature.
- Never document a feature that is not shipped and verified. Aspirational
  repos must carry an explicit status warning (see shelfseer).

## Naming notes (for new repos)

- Family suffixes are reserved: `-tile` belongs to the tile family.
- The `mark-` prefix is retired (markmint → motifmint cleared it for marktile).
