# ObstaDiff — project page

Project page for **ObstaDiff: Generalizable Diffusion Policy Learning via
Obstacle-aware Representations** (Wang, Yao, Jawed — CoRL 2026).
[arXiv:2609.10918](https://arxiv.org/abs/2609.10918)

Built on the
[Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template),
laid out like [ProbeGen](https://vision.huji.ac.il/probegen/). Static files, no
build step.

## Preview

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

## Layout

```
index.html                     the whole page
static/css/index.css           upstream template stylesheet + a short
                               "project-specific additions" block at the end
static/js/index.js             upstream template script (null-guarded, see below)
static/css/, static/js/        vendored Bulma, bulma-carousel, bulma-slider, Font Awesome
static/webfonts/               Font Awesome webfonts
static/images/                 figures extracted from the paper PDF
static/pdfs/obstadiff.pdf      the preprint, linked from the "Paper" button
```

## Sections

Header · teaser (Fig. 1) · Abstract · Method (Fig. 2) · Experimental Setup
(Fig. 3) · Results (Table 1) · Ablations (Fig. 4) · TOB Preprocessing (Fig. 5) ·
BibTeX · footer.

All figures and numbers are pulled straight from the paper. The only
placeholders left are marked `TODO` in `index.html`:

- author homepage links (`AUTHOR_HOMEPAGE`, three of them)
- the GitHub repo URL (`YOUR_REPO_HERE`) — delete the block if there is no code release
- the deployed URL (`YOUR_DOMAIN.com`) in the Open Graph / Twitter / JSON-LD tags
- the Twitter handles, or delete those two `<meta>` lines

## Optional sections

The template's **rollout video carousel** and **YouTube presentation** blocks are
kept as an HTML comment just above the BibTeX section. Paste either back in where
you want it — bulma-carousel and its CSS are already vendored, so they work as-is.
Put clips in `static/videos/` and encode with faststart so they start before they
finish downloading:

```bash
ffmpeg -i in.mov -vcodec libx264 -crf 24 -pix_fmt yuv420p -movflags +faststart -an out.mp4
```

## Regenerating the figures

The images under `static/images/` are cropped from `static/pdfs/obstadiff.pdf`
with PyMuPDF at 4× zoom and auto-trimmed. If the paper is revised, re-run that
extraction rather than editing the PNGs.

## Deviations from the upstream template

Small, deliberate, and worth knowing about if you ever diff against upstream:

- **`static/js/index.js`** — three null guards added. The upstream script assumes
  the scroll-to-top button and the "More Works" dropdown are in the DOM; this page
  (like ProbeGen) has neither, so the handlers would throw on every scroll and
  every Escape keypress.
- **`static/css/index.css`** — upstream is byte-for-byte unmodified; everything new
  is appended below a marked comment. That block adds the results-table styling and
  two layout fixes: Bulma's `.hero` is a flex container, so a `.container` inside it
  is a flex item that will not shrink below its content, which let the wide results
  table drag the page past the viewport on phones (and `html { overflow-x: hidden }`
  then clipped it with no way to scroll).
- **Font Awesome** is loaded via the vendored CSS + webfonts only. Upstream also
  loads `fontawesome.all.min.js` (1.5 MB) on top of the CSS; it renders the same
  icons.
- **Adobe DocumentCloud view SDK** is not loaded — it only exists upstream for the
  poster-PDF embed, and there is no poster section here.

## Deploy

GitHub Pages: push to `main`, then set Settings → Pages → Source to *GitHub
Actions* (`.github/workflows/deploy-pages.yml` is included). For a custom domain,
add a `CNAME` file with the bare hostname. Any static host works too.

## Licence

Website source: [CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/),
per the template. The footer attribution back to the Academic Project Page
Template is a condition of reusing it — please leave it in place.
