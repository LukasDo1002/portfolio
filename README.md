# Lukas — portfolio site

A static portfolio with a floating project field, project dossiers, and a
"Workbench" log for work in progress. No build step, no framework, no server —
just files. All content lives in `content/*.json` and is edited through a free
web GUI (Pages CMS).

**Total cost: €0.** Optional custom domain: ~€10/year.

---

## 1. Put it on GitHub (one time, ~5 min)

1. Create a free account at github.com (if you don't have one).
2. New repository → name it e.g. `portfolio` → keep it **public** (or private, both work).
3. On the repo page: **Add file → Upload files** → drag this whole folder's
   contents in (including the hidden `.pages.yml`) → Commit.

That's it — GitHub is now the single source of truth for your site.

## 2. Deploy with Cloudflare Pages (one time, ~5 min, free)

1. Free account at dash.cloudflare.com → **Workers & Pages → Create → Pages →
   Connect to Git** → pick your repo.
2. Build settings: framework preset **None**, build command **empty**,
   output directory **/** (root). Deploy.
3. You get a URL like `lukas-portfolio.pages.dev`. Every time the repo changes,
   the site redeploys itself within ~30 seconds.

(Netlify or GitHub Pages work the same way if you prefer them. Cloudflare's
free tier has unlimited bandwidth, which is nice for image-heavy art sites.)

**Custom domain (optional):** buy e.g. `lukas.studio` (~€10/yr, Cloudflare
sells at cost) → Pages → Custom domains → add it. HTTPS is automatic.

## 3. Edit content with Pages CMS (your GUI)

1. Go to **pagescms.org** → Sign in with GitHub → select your repo.
2. You'll see two sections, defined by `.pages.yml`:
   - **Projects** — questionnaire-style forms: title, year, category dropdown,
     blurb, cover image upload, description paragraphs, and a media list
     (images / YouTube / Vimeo / direct .mp4). Drag items to reorder.
   - **Workbench** — date, title, note, optional video. Newest shows first.
3. **Save** commits straight to GitHub → Cloudflare redeploys → live in ~30 s.

It works in Safari on your iPhone, so you can post a Workbench entry from the
studio floor.

## 4. Getting videos online from your iPhone

Honest answer first: **iCloud shared folders won't work** for this — Apple
doesn't give out direct, embeddable .mp4 links. The smoothest free pipeline:

**Recommended: unlisted YouTube**
1. Shoot the clip → open the YouTube app → upload → visibility **Unlisted**
   (only people with the link/embed see it, it's not searchable).
2. Copy the video ID (the part after `watch?v=`).
3. Open pagescms.org on your phone → Workbench → new entry → source
   `youtube` → paste the ID → Save. Done — phone to website in two minutes,
   and YouTube pays for all the bandwidth and transcoding.

**Alternatives**
- **Vimeo** (free tier): same flow, source `vimeo`, nicer player, weekly
  upload limits.
- **Your own NAS later:** once your Nextcloud is running, a public share's
  direct-download link to an .mp4 works with source `file`. Good for full
  control, but your Pi then serves every viewer's bandwidth — keep YouTube
  for anything you expect people to actually watch.

## 5. Things to personalize

- `index.html`: the email / Instagram / Are.na links in the Info panel, and
  the wordmark if you want your surname in it.
- Replace empty `cover` fields with photos via the CMS — projects without a
  cover get an auto-generated pattern.

## 6. Previewing locally

Browsers block `fetch()` from plain files, so double-clicking `index.html`
shows a notice instead of projects. In a terminal, from this folder:

    python3 -m http.server

then open http://localhost:8000. (Or just push to GitHub and look at the
deployed site — it redeploys fast enough to use as a preview.)

## File map

    index.html              the whole site (layout, styles, behavior)
    content/projects.json   all project content  ← edited by the CMS
    content/workbench.json  WIP log entries      ← edited by the CMS
    media/                  uploaded images land here (via the CMS)
    .pages.yml              defines the CMS editing forms
