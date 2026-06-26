@AGENTS.md

# Project: Personal portfolio site

Built on al-folio (Jekyll theme), deployed via GitHub Pages at https://shilpitha-03.github.io (repo renamed 2026-05-20).
Inspired by https://rohitbandaru.github.io/ — clean, technical, blog-forward.

## About me

- Robotics MSE student at Johns Hopkins University (expected 2027)
- Research focus: perception, embodied AI / physical AI
- Coursework: Deep Learning (A+), Computer Vision (A-), Deep RL
- B.Tech in Automation & Robotics Engineering from Amrita (2021–2025), CGPA 9.02/10
- Research experience:
  - IIIT Hyderabad — vision-based UAV obstacle detection, MPC controllers (Jan–Jul 2025) 
  - IIT Palakkad 
- Publication: VQ-VAE-based trajectory generation for multi-drone coordination, ICCA 2025 {https://scholar.google.com/citations?view_op=view_citation&hl=en&user=VVR4eaoAAAAJ&authuser=2&citation_for_view=VVR4eaoAAAAJ:u-x6o8ySG0sC}
- Course Assistant for Computer Vision at JHU (Spring 2026)

## Career goals (drives content priorities on this site)

- **Primary:** industry roles in perception / embodied AI / physical AI as a new grad
- **Secondary:** PhD admission in the same areas
- Site should serve both audiences: recruiters scanning for hireable signal, and PhD admissions readers looking for technical depth and writing ability

## Site scope (v1)

Three navbar sections only:
- **About** — short intro, photo, what I work on, links (LinkedIn, GitHub, email)
- **CV** — resume content rendered from `_data/cv.yml`; PDF download link to `assets/pdf/Shilpitha-Resume.pdf`
- **Blog** — technical posts on robotics, perception, physical AI; cheatsheets for frameworks I'm learning

Hide from the navbar for now (keep template files in repo, switch on later):
- Projects — re-enable when I have 2–3 strong writeups
- Publications — re-enable when ICCA paper is indexed on Google Scholar
- News, teaching, repositories — not relevant yet

## Conventions

- Blog posts live in `_posts/` as `YYYY-MM-DD-title.md` with proper frontmatter
- Blog post examples (math, code, jupyter, tables, images, charts, etc.) preserved in `_drafts/` from al-folio — copy + adapt one when writing a new post; production builds exclude `_drafts/` by default (preview locally with `jekyll serve --drafts`)
- Always show me diffs before applying multi-file changes
- I'm new to Jekyll/Liquid — when you do something non-obvious, briefly explain why
- Prefer minimal config changes; flag any structural changes before making them
- When I ask "how do I do X," default to explaining rather than just doing — I'm learning, not just shipping
- For any new dependency, library, or build step you add, tell me what it does and why we need it
- Commit messages: imperative mood, concise (e.g., "Add CV page" not "Added the CV page yesterday")

## What "done" looks like for v1

- Live site at `<username>.github.io` with About, CV, and Blog in the nav
- About page has my photo, a paragraph bio, working social links
- CV page renders my actual resume content and offers PDF download
- At least one published blog post (I have an idea on writing it about filters and applications in the robotics sense. will work on the content thoroughly once we have a preliminary site published)
- Mobile-responsive, dark mode toggle working, no broken links

## v1 status — shipped 2026-05-21

**Live at:** https://shilpitha-03.github.io/

**Built in 19 commits.** Three pages in navbar — About, Blog, CV.

| Page | What's there |
|---|---|
| About (`/`) | Bio, photo + affiliation block, selected publication (DISCO ICCA 2025), social icons (Email · GitHub · LinkedIn · Scholar) |
| CV (`/cv/`) | Structured resume rendered from `_data/cv.yml`, downloadable PDF |
| Blog (`/blog/`) | "Coming soon" placeholder; al-folio demo posts moved to `_drafts/` as a feature-reference library |

## Roadmap for v2 and beyond

Deferred from v1 with their re-enable path:

- **First blog post (filters in robotics).** Add a file at `_posts/YYYY-MM-DD-filters-in-robotics.md` (copy a `_drafts/` example as a template — e.g., `2015-10-20-math.md` for LaTeX-heavy posts, `2023-07-04-jupyter-notebook.md` for notebook-style writing). Then flip `latest_posts.enabled: true` in `_pages/about.md`.
- **Re-enable RSS** when posts exist: uncomment `rss_icon:` in `_data/socials.yml` (restores RSS icon on about + "RSS Feed" in Ctrl+K).
- **Re-enable Publications page** when you have 3+ papers: set `nav: true` in `_pages/publications.md`. Each paper is a BibTeX entry in `_bibliography/papers.bib`.
- **Re-enable Projects page** when 2–3 strong writeups are ready: set `nav: true` in `_pages/projects.md`; each writeup is a file in `_projects/`; also remove `projects` from `search_excluded_collections` in `_scripts/search.liquid.js`.
- **Re-enable News/announcements** when there's news worth showing: set `nav: true` in `_pages/news.md` and `announcements.enabled: true` in `_pages/about.md`; each item is a file in `_news/`; also remove `news` from `search_excluded_collections`.
- **Auto-render CV PDF** via `.github/workflows/render-cv.yml` so editing `_data/cv.yml` regenerates the PDF (tradeoff: RenderCV typography vs. a hand-crafted PDF).
- **Custom domain.** Point a domain at GitHub Pages via a `CNAME` file in repo root + DNS records.
- **Fix Prettier CI.** Run `npx prettier . --write` and commit; removes the persistent red ❌ on every push (informational, doesn't block deploy).
- **Photo to circular crop.** Set `image_circular: true` in `_pages/about.md` once the photo is a clean square.
- **Delete `books:` collection.** When you're sure: remove from `collections:` in `_config.yml`, delete `_books/` and `_pages/books.md`.

## Where to make changes (edit guide)

| What you want to change | File(s) to edit |
|---|---|
| Site name, URL, description, keywords, contact note | `_config.yml` ("Site settings" section, top of file) |
| Profile photo | Replace `assets/img/prof_pic.jpg` (keep filename) |
| Bio paragraphs | `_pages/about.md` — body, everything after the closing `---` of frontmatter |
| About-page subtitle (under page title) | `_pages/about.md` frontmatter, `subtitle:` |
| Affiliation block (under photo) | `_pages/about.md` frontmatter, `profile.more_info:` |
| Toggle about-page sections (selected papers, announcements, latest posts) | `_pages/about.md` frontmatter — `selected_papers`, `announcements.enabled`, `latest_posts.enabled` |
| Social icons (which appear, their values) | `_data/socials.yml` — slugs/IDs only; URLs are auto-built |
| Selected publications source | `_bibliography/papers.bib` — BibTeX entries with `selected={true}` render on about page |
| Author name bolding in citations | `_config.yml`, `scholar.last_name` / `scholar.first_name` arrays (multi-name supported) |
| CV header (name, email, phone, location, summary, social links) | `_data/cv.yml`, top-level `cv:` block |
| CV sections (Education, Experience, Projects, Publications, Skills) | `_data/cv.yml`, under `cv.sections:` |
| CV downloadable PDF | Replace `assets/pdf/Shilpitha-Resume.pdf`; if renaming, update `cv_pdf:` in `_pages/cv.md` |
| Blog page title / tagline | `_config.yml` — `blog_name`, `blog_description` |
| Add a blog post | Create `_posts/YYYY-MM-DD-title.md`; see `_drafts/` for feature examples by file name |
| Show/hide a page in navbar | `_pages/<page>.md` frontmatter, `nav: true` or `nav: false` |
| Theme defaults (dark mode, MathJax, masonry, etc.) | `_config.yml`, "Optional Features" section (`enable_X` flags) |
| Ctrl+K palette exclusions | `_scripts/search.liquid.js`, `search_excluded_collections` list |
| Page layouts (rarely needed) | `_layouts/<name>.liquid` |
| Reusable HTML snippets | `_includes/<name>.liquid` |
| Site styling (rarely needed) | `_sass/*.scss` |

**Publishing flow for any edit:** `git add <file>` → `git commit -m "..."` → `git push`. The deploy workflow (`.github/workflows/deploy.yml`) auto-builds and publishes within 2–4 minutes. Hard-refresh the live URL (Ctrl+Shift+R) to bypass browser cache.

## Collaboration guidelines (reusable across projects)

The block between the horizontal rules below is **project-agnostic** — copy it verbatim into any future project's `CLAUDE.md` (or equivalent agent guidance file) to set up the same collaboration style with Claude Code.

---

### Working style

- **One file per edit, one commit per edit.** Don't batch multi-file changes unless I explicitly ask. Each unit of work should map cleanly to a single concise commit message.
- **Commit messages: imperative mood, concise** (e.g., "Add login page" not "Added the login page"). Always propose the commit message *before* the edit so I can sanity-check intent. Before I prompt an edit, the question I ask myself is: "what's the commit message going to be?" — if that isn't crisp, the scope is wrong.
- **Before any edit, explain in plain terms** what you'd change, where, and why. Wait for me to approve before doing it. Pure read-only exploration (reads, greps, lists, `git status`) does not need pre-approval.
- **Show diffs before applying multi-file changes.**
- **Maintain a running build log in this file.** After every commit, append a one-line entry to a `## Build log` section: date, commit subject, file(s) touched, one-line note on the decision behind it. Treat the log entry as part of the same commit as the change it describes.

### Teaching mode

- When I ask "how do I do X," **default to explaining rather than just doing** — I'm learning, not just shipping.
- When you do something non-obvious, **briefly explain why**.
- For any new dependency, library, or build step you add, **tell me what it does and why we need it**.
- Prefer concrete file paths and clickable links over abstract guidance.

### Asking vs. acting

- **When my prompt is ambiguous, ask one clarifying question** instead of guessing.
- **Never make destructive changes (deletes, force-pushes, schema migrations, irreversible config flips) without explicit approval**, even if implied by an earlier instruction.
- **Flag any structural changes before making them.**

### My learning goals (apply to every interaction)

Two skills I'm actively practicing:
1. **Writing unambiguous prompts** — when my prompt could have been clearer, gently surface that.
2. **Reviewing diffs intuitively and making informed decisions** — when presenting a diff, point out what to look at and why.

---

## Build log

_Format: `date` — `commit subject` — files touched — one-line note. Chronological, oldest first._

- `2026-05-20` — `Tidy CLAUDE.md and add build log section` — `CLAUDE.md` — Removed duplicate `@AGENTS.md` import, set canonical site URL to `shilpithathokala.github.io`, added this Build log section.
- `2026-05-20` — `Set site identity in _config.yml` — `_config.yml` — Replaced upstream al-folio defaults (`description`, `keywords`, `url`, `baseurl`, `contact_note`) with personal values; left name fields, footer, icon, scholar config untouched (scholar still set to Einstein — fix when re-enabling Publications).
- `2026-05-20` — `Hide unused sections from navbar` — `_pages/projects.md`, `_pages/publications.md`, `_pages/teaching.md`, `_pages/repositories.md` — Set `nav: false` on four pages to leave only About, CV, Blog in the navbar; news.md already had no `nav:` key, so left untouched.
- `2026-05-20` — `Add LinkedIn, GitHub, email, Scholar links` — `_data/socials.yml` — Set personal email, GitHub (`shilpitha-03`), LinkedIn (`shilpitha-chowdary-t03`), and Scholar user ID (`VVR4eaoAAAAJ`); commented out `inspirehep_id` and `custom_social` (Einstein placeholders that would have rendered icons pointing to the wrong profiles).
- `2026-05-20` — `Add profile photo` — `assets/img/prof_pic.jpg` — Replaced theme's Einstein demo photo with personal square-cropped headshot at the same path so `_pages/about.md`'s default `image: prof_pic.jpg` reference works without further edits.
- `2026-05-20` — `Update site URL after repo rename to shilpitha-03.github.io` — `_config.yml`, `CLAUDE.md` — Repo renamed on GitHub from `shilpithathokala.github.io` to `shilpitha-03.github.io` to convert from project site (broken assets, ugly URL) to user site at `https://shilpitha-03.github.io/`. Updated `url:` in `_config.yml` and the URL reference at top of CLAUDE.md. Local `.git/config` remote URL also updated via `git remote set-url` (not a tracked change).
- `2026-05-20` — `Hide remaining demo navbar entries` — `_pages/dropdown.md`, `_pages/profiles.md` — Set `nav: false` on the "submenus" dropdown (which carried the "bookshelf" child entry) and the "people" profiles page; completes the navbar trim missed in the earlier Step 3 pass, leaving only About · Blog · CV.
- `2026-05-20` — `Remove RSS and CV icons from about page socials` — `_data/socials.yml` — Commented out `cv_pdf` (CV page has its own download button, icon was an extra path) and set `rss_icon: false` (no blog posts yet, also visually redundant). About-page social row now: Email · GitHub · LinkedIn · Scholar.
- `2026-05-20` — `Write about page bio` — `_pages/about.md` — Replaced template placeholders with real subtitle (`MS student in Robotics at JHU.`), affiliation block (Whiting / JHU / Baltimore, MD), and three-paragraph bio with inline links to `/cv/`, `/blog/`, `mailto:sthokal1@jh.edu`. Toggled off `selected_papers` (ICCA not on Scholar yet), `announcements` (news hidden from nav), and `latest_posts` (no real posts yet) — all three flagged to re-enable later when content is ready.
- `2026-05-20` — `Add ICCA 2025 paper to selected publications` — `_bibliography/papers.bib`, `_config.yml`, `_pages/about.md` — Deleted five Einstein demo entries and added DISCO (Teja et al., ICCA 2025) with `selected={true}` and `bibtex_show={true}`. Updated `scholar.last_name`/`first_name` to recognize "Chowdary" and "Thokala" forms so the user's name is bolded in the rendered citation. Flipped `selected_papers: false → true` on about. Corrected the bio prose — the paper is diffusion-based (DISCO), not VQ-VAE-based as originally written.
- `2026-05-21` — `Populate CV data` — `_data/cv.yml` — Replaced Einstein placeholders with structured CV from user's resume: 2 education entries (JHU MSE, Amrita B.Tech), 3 experience entries (IIIT Hyderabad, IIT Palakkad, JHU Course Assistant), DISCO publication, 4 projects (Neural Deblurring with GitHub link, UVMS, omniwheel bike, wrist rehab), 4 skill categories. Phone, school email, and Baltimore location in header. Paper title rendered as DISCO; user fixing resume PDF separately (old VQ-VAE title + old portfolio URL) before we wire the CV download in step 8.
- `2026-05-21` — `Add CV PDF download` — `_pages/cv.md`, `assets/pdf/Shilpitha-Resume.pdf` — Pointed `cv_pdf:` at the user-provided resume PDF (corrected DISCO title + portfolio URL) and removed the demo `description:` line so the CV page no longer shows the "modify it in `_pages/cv.md`" placeholder under the title. Theme's `example_pdf.pdf` left in `assets/pdf/` for now (separate cleanup if user wants it gone).
- `2026-05-21` — `Remove theme demo PDF` — `assets/pdf/example_pdf.pdf` — Deleted leftover al-folio example PDF that was no longer referenced anywhere; reduces noise in the deploy artifact.
- `2026-05-21` — `Move demo blog posts to _drafts/ for future reference` — `_posts/` → `_drafts/` (31 files), `CLAUDE.md` — Relocated all al-folio demo posts so they no longer render on the blog page but remain in the repo as a feature reference library (math, code, jupyter, tables, charts, etc.). Added a pointer note in CLAUDE.md Conventions. Jekyll excludes `_drafts/` from production builds by default; preview locally with `jekyll serve --drafts`.
- `2026-05-21` — `Configure blog page as 'coming soon' placeholder` — `_config.yml` — Set `blog_name: blog` and `blog_description: coming soon — writing on perception, embodied AI, and the frameworks i'm picking up.`; cleared `display_tags`/`display_categories` (had pointed at demo-post tags which would render as broken-link pills now that posts are in `_drafts/`).
- `2026-05-21` — `Disable al-folio external blog post sources` — `_config.yml` — Replaced the theme-default `external_sources` block (Medium feed `medium.com/@al-folio` + hardcoded Google Blog post) with `[]`. Removed the two filler posts ("Google Gemini..." and "Displaying External Posts on Your al-folio Blog") from the blog page and from the Ctrl+K Posts section.
- `2026-05-21` — `Trim Ctrl+K search palette to v1 scope` — `_data/socials.yml`, `_scripts/search.liquid.js` — Commented out `rss_icon` entirely (mere key presence — regardless of `false` value — was triggering a "RSS Feed" entry under Ctrl+K Socials). Added `books, news, projects, teachings` to a `search_excluded_collections` list in `search.liquid.js` so those collection items no longer surface as Ctrl+K sections; underlying collections remain in `_config.yml` so News/Projects can be re-enabled cleanly when v2 has content.
- `2026-05-21` — `Document v1 status, edit guide, and reusable collaboration rules` — `CLAUDE.md` — Final v1 closeout commit. Added three sections: (a) "v1 status" + "Roadmap for v2 and beyond" capturing what shipped and what's deferred with re-enable paths; (b) "Where to make changes" table mapping each portfolio surface to the file(s) that control it; (c) "Collaboration guidelines (reusable across projects)" — a project-agnostic block delimited by horizontal rules, formatted for copy-paste into future projects.
- `2026-05-21` — `Add notes.md scratch space (excluded from Jekyll build)` — `notes.md`, `_config.yml`, `CLAUDE.md` — Created `notes.md` at repo root for accumulating reading/learning notes. Added to `_config.yml` `exclude:` list so Jekyll never builds it (file is on GitHub but not on the live site). Workflow: dated entries in `notes.md` → harvest section into `_drafts/YYYY-MM-DD-title.md` → move to `_posts/` when ready to publish.
- `2026-06-26` — `Add research projects and update CV coursework and skills` — `_data/cv.yml` — Folded new resume content into the existing CV (kept richer site version per user). Prepended 3 research projects to `Projects:` — affordance view-consistency diagnosis, surgical multimodal RAG, and VLA affordance probing — using `summary:` to carry each one's "graduate research" descriptor (the project renderer ignores dates; a custom "Research Projects" section name would fall to the generic renderer and not display name/highlights, so they live under `Projects:`). Swapped coursework `Deep RL → Learning Based Vision` (kept A+/A- grades). Added `VLMs & VLA models, diffusion models, DINOv2` to ML/Vision skills. Left Selected Projects, Course Assistant placement, fuller experience bullets, and the accurate DISCO publication title unchanged.
- `2026-06-26` — `Update resume PDF and point CV download at new filename` — `_pages/cv.md`, `assets/pdf/*`, `notes.md` — User replaced the resume PDF under a new filename (`Shilpitha_Thokala_Resume.pdf`, underscores) and updated `cv_pdf:` to match; old `Shilpitha-Resume.pdf` deleted. Their `git add .`/`git push` had staged but never committed it (no `git commit` step), so the deploy didn't pick it up — committed + pushed here. `notes.md` scratch edits got swept into the same commit (harmless: build-excluded, already tracked).
- `2026-06-26` — `Link new research project repos in CV` — `_data/cv.yml` — Added `url:` to the two new research projects whose repos now have real READMEs (verified live via WebFetch): `ViewConsistency_affordance` and `VLA-affordance`. Surgical RAG left unlinked (paper unpublished); Neural Deblurring link unchanged.