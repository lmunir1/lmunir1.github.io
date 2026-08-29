# Personal Homepage — Design Spec

**Repo:** `lmunir1.github.io` (personal GitHub Pages site)
**Date:** 2026-08-29

## Background

`index.html` in this repo currently hosts the RDS Risk Calculator and AMD Clinical
Decision Support tool, branded as a "Paulus Lab — Clinical Decision Support" page.
It is not a personal homepage. This spec covers replacing it with an actual
personal site: bio, research experience, project portfolio, publications, contact.

**Out of scope (separate sub-project):** moving `rds-calculator.html` and
`amd-tool.html` out of this repo into the `PaulusLab.github.io` repo under a
`/tools` subpage. That work happens independently and isn't part of this spec —
this spec's project cards link out to those tools' new home once it exists, but
does not build that home.

## Goals

- Replace `index.html` with a single-page personal site: bio + research experience
  up top (academic framing), project portfolio below (builder framing) — the
  "hybrid" tone the user asked for.
- Visual identity: **Warm Editorial** — cream background, warm amber/terracotta
  accent, serif headline with an italic subhead, sans-serif body. Approved via
  the visual companion (see mockups in `.superpowers/brainstorm/`).
- Self-contained static HTML/CSS, no build step, no framework dependency. The
  new `index.html` does not use Tailwind — that script stays in `vendor/` only
  because `rds-calculator.html`/`amd-tool.html` still depend on it until they
  move to the lab repo; this page reuses just the vendored Inter font files.
- Curated, not exhaustive: this page highlights; the full CV (updated
  separately) is one click away as a PDF download for anyone who wants the
  complete list of experience, certifications, presentations, and all 21
  publications.

## Visual Design

- **Palette:** background `#faf6ee` (cream), primary text `#2b2620` (near-black
  warm gray), secondary text `#5c5548`, accent `#b45309` (terracotta/amber),
  hairline borders `#e8dfc8`.
- **Typography:** headline serif — Google Fonts **"Fraunces"** (has real
  italics, warmer/more editorial than generic Georgia, self-hosts fine since
  this is a real deployed site, not a sandboxed artifact). Body/UI sans — reuse
  the **Inter** font already vendored locally in this repo
  (`vendor/fonts/inter/`), so body text doesn't add a new network dependency.
- **Hero:** small uppercase eyebrow ("Wilmer Eye Institute · Baltimore"), large
  serif name, italic serif tagline, one-paragraph sans-serif intro, two buttons
  (View Projects / Download CV — solid terracotta + outlined terracotta).
- Section labels throughout: small uppercase sans-serif in the accent color,
  consistent with the hero eyebrow — this is the recurring visual motif tying
  sections together.

## Page Structure (single page, in order)

1. **Hero** — name, tagline, one-paragraph intro, CTA buttons.
2. **About** — one paragraph adapted from the CV's Professional Summary,
   written in first person, warmer/less resume-toned than the CV version.
3. **Research Experience** — condensed list (not full CV detail) of current
   roles:
   - Paulus Lab, Retina Department — Research Intern, 07/2025–present
   - Wilmer Glaucoma ML Lab (Dr. Yohanan) — Visiting Student, 09/2025–present
   - Wilmer Eye Research Institute (Dr. Fasika Woreta) — Visiting Student,
     09/2025–present
   Each as a one-line role + one-line focus, no bullet-level CV detail. Closing
   note pointing to the CV download for full detail.
4. **Projects** — five featured cards, in this exact order (confirmed by user):
   1. **RDS Risk Calculator** — elastic-net regression model (propensity-score-
      matched variable screening) predicting 180-day outcomes after RRD repair;
      deployed as a public web calculator. Link → lab site `/tools` page once
      it exists (placeholder link/label until then, see Open Items).
   2. **OCT Segmentation Pipeline** — SegFormer-B4 deep learning segmentation
      model with MONAI Label active learning, automatically segmenting retinal
      detachment biomarkers on OCT images.
   3. **RD OCT Biomarker Model** — downstream model that takes the segmented
      biomarkers from the pipeline above and predicts an outcome from them
      (distinct project from the segmentation step itself).
   4. **AMD CDS Tool** — clinical decision support tool for age-related macular
      degeneration. Link → lab site `/tools` page (same placeholder situation
      as the RDS calculator).
   5. **Lab Research Dashboard** — full-stack project/task/conference/resource
      management platform (Next.js, PostgreSQL) built and deployed for
      lab-wide use, including a mobile-optimized interface. (Renamed from
      "Paulus Lab Research Dashboard" — shorter, PI-agnostic name.)

   Explicitly **excluded** from the homepage entirely (user's call): the RRD
   EHR Extraction Pipeline, the Woreta Lab Research Dashboard, and the
   Ophthalmology Faculty Outreach Agent.

   Each card: project name, 1–2 sentence description, tech-stack tag line. No
   screenshots for v1 (none available) — clean text cards matching the
   approved wireframe.
5. **Selected Publications** — 3–4 highlighted papers (not all 21):
   - Xie X, Munir L, Paulus YM. *Retinal Laser Therapy Mechanisms, Innovations,
     and Clinical Applications.* Photonics. 2025.
   - Munir L, et al. Efficacy and safety of LipiFlow® ... meta-analysis. *Ocul
     Surf*. 2024.
   - Munir L, Chaudhary AJ, et al. Trend analysis of kidney stone-related
     mortality, 1999-2020. *J Am Soc Nephrol*. 2024.
   Followed by "View all 21 publications on Google Scholar →" linking to
   https://scholar.google.com/citations?user=wp3qUZAAAAAJ&hl=en
6. **Contact / Footer** — email (`lmunir2@jh.edu`, mailto), GitHub
   (github.com/lmunir1), Google Scholar (link above), Download CV (PDF).

## CV PDF

The updated `CURRICULUM VITAE.docx` (already revised this session) gets
exported to PDF and committed into this repo (e.g. `assets/Luqman-Munir-CV.pdf`)
so the "Download CV" buttons have something to point to. Regenerating that PDF
is part of implementation, not a manual step left to the user.

## Technical Approach

- Single `index.html`, inline `<style>` (matches the existing repo's pattern in
  the current index.html/rds-calculator.html — no separate CSS file needed for
  a page this size).
- No JavaScript required — this is a static content page, not an interactive
  tool. (Compare: the tools being removed are legitimately interactive and
  keep their own JS; this page doesn't need any.)
- Responsive via CSS flexbox/grid + relative units; project cards collapse
  from a multi-column grid to single column on narrow viewports.
- `vendor/` directory (Tailwind script + Inter font files) stays in the repo
  only as long as `rds-calculator.html`/`amd-tool.html` still live here; once
  those move to the lab repo (separate sub-project), `vendor/`'s Tailwind
  script becomes unused and can be removed, but Inter font files stay (this
  page uses them for body text).

## Testing / Verification

- Open the page in the browser tool at both desktop and mobile widths, confirm
  layout doesn't break, links resolve (mailto, GitHub, Scholar, CV PDF
  download), and the CV PDF actually opens/downloads correctly.
- No automated tests — static content site.

## Open Items

- **Tools links are placeholders until the lab-site `/tools` sub-project
  happens.** For now, the RDS Risk Calculator and AMD CDS Tool cards will link
  to their *current* location in this repo (`rds-calculator.html`,
  `amd-tool.html`) so the links aren't dead; update these two links when the
  lab-site tools page ships.
- No profile photo provided — hero stays text-only.
