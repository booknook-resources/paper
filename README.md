# paper

Stickers and paper scans from book nook kits.

## Layout

- **`src/<kitId>/metadata.json`** — **Source of truth** for that kit: `name`, `link`, `manufacturer`, `notes`. The kit id is always the **folder name**; it is not stored in `metadata.json` and is filled in when compiling `kits.json`.
- **`src/<kitId>/`** — Scanned PDFs, images, and other resource files for that kit (everything except ignored names such as `README.md` and `metadata.json`).
- **`src/<kitId>/README.md`** — Human-readable notes for the kit (linked from the generated index).

## Compiled catalog

- **`kits.json`** (repository root) — **Generated**: merged array of every `src/<kitId>/metadata.json`. Do not edit by hand; run the generator or merge to `main` and let CI refresh it.

## Generated documentation

[`docs/resources.md`](docs/resources.md) is **auto-generated**: a list of resources grouped by manufacturer, then kit name, with relative links (no image previews). Do not edit it by hand.

On every push to `main` that touches `src/`, the generator, or this workflow, [`.github/workflows/generate-resources.yml`](.github/workflows/generate-resources.yml) rebuilds **`docs/resources.md`** and **`kits.json`** and commits updates when needed (commit message includes `[skip ci]` to avoid an infinite workflow loop).

You can also run the generator locally:

```bash
python3 scripts/generate_resources.py
```

On Windows, if `python3` is not on your `PATH`, use `py -3 scripts/generate_resources.py`.

## Adding a kit

1. Create `src/<kit-id>/`.
2. Add **`metadata.json`** with the catalog fields (`name`, `link`, `manufacturer`, `notes`). Do not put `kitId` there; it is inferred from `<kit-id>`.
3. Add **`README.md`** and scan files as needed.
4. Run the generator (or merge to `main` and let CI run).

Every directory directly under `src/` must include **`metadata.json`**.
