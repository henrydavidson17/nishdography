# nishdography — how this site works

Your whole website is three things:

1. **index.html** — the entire site: layout, styling, gallery, filters, lightbox, and edit mode, all in one file you can read top to bottom.
2. **photos.json** — the catalogue. Every photo gets one entry: its filename, caption, film/digital, subjects, and date. The order of entries in this file *is* the "My order" sort on the site.
3. **photos/** — a folder containing the actual image files.

The site never needs rebuilding or compiling. Change photos.json, refresh the page, done.

## Putting it online (GitHub Pages, free, no command line)

1. Make a free account at github.com if you don't have one.
2. Click **New repository**, name it something like `nishdography`, set it to Public, and create it.
3. Click **uploading an existing file** (or Add file → Upload files) and drag in `index.html`, `photos.json`, and your `photos` folder. Click **Commit changes**.
4. Go to **Settings → Pages**, and under "Branch" choose `main` and save.
5. After a minute or two your site is live at `https://YOURUSERNAME.github.io/nishdography/`.

Every future update is the same upload-and-commit motion, and GitHub keeps a full history, so nothing is ever lost and you can see exactly what changed — a good habit to absorb early.

## The Google Photos → website workflow

1. In Google Photos, select the shots you want and download them (the ⋮ menu, or Shift+D). They arrive as a zip — unzip it.
2. Optional but worth it: shrink them first. Full-resolution files make the site slow. Drag the batch through squoosh.app or any resizer at ~2000px on the long edge.
3. Open your live site, click **Edit**, then **+ Add photos**, and pick those same files. The site reads their names and dimensions and creates catalogue entries (you'll see them appear, previewed from your computer).
4. Still in edit mode: click **✎ edit** on each new photo to set caption, film or digital, film stock, subjects, and date. Drag photos around to set the order.
5. Click **Download photos.json**.
6. On GitHub: upload the new image files into the `photos` folder, and upload the new `photos.json` to replace the old one. Commit. Refresh your site.

That's the whole loop — roughly five minutes per batch, and no code touched.

## Tagging model

Each photo has one **format** (`film` or `digital`, with an optional `film_stock` like "Portra 400") and any number of **subjects** (`travel`, `street`, `architecture`, `fam & friends`, `edgy`, `linos`, or anything new you type in the edit panel — new tags automatically become filter buttons). Film photos get an amber film-rebate strip in the lightbox; digital ones get a quieter grey strip.

## Reading the code (since you said you wanted to learn)

index.html is organised into numbered, commented sections. A decent path through it:

- Section 1 (design tokens) — every colour and font is a named variable; change `--rebate` and watch the accent colour change everywhere.
- The `SAMPLE` constant and `load()` — how the site fetches photos.json and falls back to sample data.
- `computeVisible()` — filtering and sorting in about ten lines; this is the heart of the site.
- `render()` — turns the data into HTML cards.
- `layout()` — the masonry trick: a grid of tiny 8px rows where each photo spans as many as it needs.

A good first exercise: change the strapline text in the header, or add a fifth sort option. Paste any section into Claude and ask "explain this line by line" — that's a genuinely effective way to learn.
