# momusic Animation Studio — pack marketplace (hosting kit)

Free hosting plan: **one public GitHub repo**. No fees, no keys,
no server. The app reads `packs.json` straight from the repo and
downloads the zips listed in it.

## One-time setup (2 minutes)

1. Create a public GitHub repo, e.g. `momusic-packs`.
2. Upload everything in this folder (`packs.json`, `packs/`,
   `thumbs/`) to the repo root, on the `main` branch.
3. Point the app at it, in code: set `catalogUrl` in
   `lib/config/marketplace_constants.dart` to
   `https://raw.githubusercontent.com/<your-name>/momusic-packs/main/packs.json`
   and build. The address is baked in — users can't change it.
   In the app, **Settings → Animation → the globe tile** opens the
   Marketplace; **Get** downloads and installs packs straight
   into the animation grid.

## Adding a pack later

1. Drop the new `.zip` into `packs/` and its preview into
   `thumbs/` (any JPG, ~360px wide).
2. Add one entry to `packs.json` (copy an existing block, change
   the fields).
3. Commit. The app sees it on its next catalog refresh — no app
   update, no redeploy.

## Rules that keep it free forever

- Keep packs small (ours are ~50–600 KB). GitHub is generous with
  small files; don't push videos or huge images.
- Never rename a published pack file — installed users' catalogs
  point at these paths. Add new files instead.

## Pack themes (from this kit onward)

Every entry in `packs.json` can carry a `theme` with three hex
colours — `accent`, `background` and `surface`:

```json
"theme": {
  "accent": "#B7D8E1",
  "background": "#24292C",
  "surface": "#6A7073"
}
```

When a user downloads the pack and selects its animation, the
app automatically wears that theme. A pack's own css `theme:`
header wins if it declares one; otherwise the catalog theme is
used. Themes are optional: an entry without one simply leaves
the app's current colours alone.
