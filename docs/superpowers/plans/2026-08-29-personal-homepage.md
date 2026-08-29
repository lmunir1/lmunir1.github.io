# Personal Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace `index.html` in the `lmunir1.github.io` repo with a single-page personal homepage (Hero, News & Updates, About, In a Nutshell, Research Experience, Projects, Selected Publications, Contact) in the approved Warm Editorial visual style.

**Architecture:** One static, self-contained `index.html` with an inline `<style>` block — no build step, no JS. Content is built up section-by-section, each section a `<section class="section">` block sharing the same design system (CSS variables, `.section-label` motif, hairline borders). A CV PDF is exported from the already-updated `CURRICULUM VITAE.docx` and committed to `assets/` so the Download CV buttons work.

**Tech Stack:** Plain HTML5 + CSS (custom properties, flexbox/grid). Google Fonts (Fraunces) for headline serif, loaded via `<link>`. The already-vendored local Inter font (`vendor/fonts/inter/inter.css`) for body text. No JavaScript.

## Global Constraints

- Palette: background `#faf6ee`, primary text `#2b2620`, secondary text `#5c5548`, accent `#b45309`, hairline borders `#e8dfc8` — from the design spec, use these exact hex values everywhere, no ad-hoc colors.
- Headline font: Google Fonts "Fraunces" (weights 400/600/700, italic 400/500). Body font: local `Inter` from `vendor/fonts/inter/inter.css` (already in the repo — do not add a second body font or a Google Fonts sans).
- No JavaScript anywhere on this page.
- Single file: all CSS lives in one `<style>` block in `index.html`. Do not create a separate `.css` file.
- Do not touch `rds-calculator.html`, `amd-tool.html`, or `vendor/` beyond what's specified — they're out of scope (moving to the lab site in a separate sub-project).
- Every external link (GitHub, Scholar, DOIs) gets `target="_blank" rel="noopener"`; internal links (`#anchors`, `assets/...`, `rds-calculator.html`, `amd-tool.html`) do not.
- Spec reference: `docs/superpowers/specs/2026-08-29-personal-homepage-design.md` in this repo — if anything here seems to conflict with it, the spec wins.

---

### Task 1: Page shell, design system, Hero, and News & Updates

**Files:**
- Create: `index.html` (overwrites the current tools-launcher page — the old content, `rds-calculator.html` and `amd-tool.html`, are unaffected since they're separate files)

**Interfaces:**
- Produces: the CSS design system (custom properties `--bg`, `--text`, `--text-secondary`, `--accent`, `--border`; classes `.container`, `.section`, `.section-label`, `.btn`/`.btn-solid`/`.btn-outline`) that every later task's HTML relies on. Later tasks must reuse these exact class names — do not invent new ones for the same visual role.

- [ ] **Step 1: Write `index.html` with full `<head>`, complete `<style>` block, and the Hero + News & Updates sections**

Overwrite `index.html` with exactly this content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Luqman Munir</title>
<meta name="description" content="Luqman Munir — medical student researcher in ophthalmology AI at Johns Hopkins Wilmer Eye Institute.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,wght@0,400;0,600;0,700;1,400;1,500&display=swap" rel="stylesheet">
<link href="vendor/fonts/inter/inter.css" rel="stylesheet">
<style>
  :root {
    --bg: #faf6ee;
    --text: #2b2620;
    --text-secondary: #5c5548;
    --accent: #b45309;
    --border: #e8dfc8;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', Arial, sans-serif;
    line-height: 1.6;
  }
  a { color: inherit; }
  .container { max-width: 760px; margin: 0 auto; padding: 0 40px; }
  .section { padding: 48px 0; border-bottom: 1px solid var(--border); }
  .section-label {
    font-family: 'Inter', Arial, sans-serif;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 16px;
    font-weight: 600;
  }
  h1, .serif { font-family: 'Fraunces', Georgia, serif; }

  /* Hero */
  .hero { padding: 64px 0 48px; }
  .hero-eyebrow { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--accent); margin-bottom: 14px; font-weight: 600; }
  .hero h1 { font-size: 40px; font-weight: 700; margin-bottom: 10px; }
  .hero-tagline { font-family: 'Fraunces', Georgia, serif; font-style: italic; font-size: 17px; color: var(--accent); margin-bottom: 18px; font-weight: 400; }
  .hero-intro { font-size: 15px; color: var(--text-secondary); max-width: 520px; margin-bottom: 26px; }
  .hero-actions { display: flex; gap: 12px; flex-wrap: wrap; }

  .btn { display: inline-block; font-family: 'Inter', Arial, sans-serif; font-size: 13px; font-weight: 600; padding: 11px 20px; border-radius: 5px; text-decoration: none; }
  .btn-solid { background: var(--accent); color: #fff; }
  .btn-solid:hover { opacity: 0.9; }
  .btn-outline { border: 1px solid var(--accent); color: var(--accent); }
  .btn-outline:hover { background: rgba(180,83,9,0.08); }

  /* News */
  .news-item { display: flex; gap: 20px; padding: 14px 0; border-top: 1px solid var(--border); }
  .news-item:first-child { border-top: none; padding-top: 0; }
  .news-date { flex: 0 0 90px; font-size: 12px; font-weight: 700; letter-spacing: 0.5px; text-transform: uppercase; color: var(--accent); }
  .news-text { font-size: 14px; color: var(--text); }

  /* About */
  .about-text { font-size: 15px; color: var(--text-secondary); max-width: 620px; }

  /* Nutshell */
  .nutshell-item { padding: 20px 0; border-top: 1px solid var(--border); }
  .nutshell-item:first-child { border-top: none; padding-top: 0; }
  .nutshell-title { font-family: 'Fraunces', Georgia, serif; font-size: 19px; font-weight: 600; margin-bottom: 6px; }
  .nutshell-text { font-size: 14px; color: var(--text-secondary); max-width: 600px; }

  /* Research Experience */
  .exp-item { padding: 16px 0; border-top: 1px solid var(--border); }
  .exp-item:first-child { border-top: none; padding-top: 0; }
  .exp-role { font-size: 15px; font-weight: 700; margin-bottom: 2px; }
  .exp-meta { font-size: 12px; color: var(--text-secondary); margin-bottom: 6px; }
  .exp-focus { font-size: 14px; color: var(--text-secondary); }
  .exp-note { font-size: 13px; color: var(--text-secondary); margin-top: 18px; }
  .exp-note a { color: var(--accent); }

  /* Projects */
  .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; }
  .project-card { background: #fff; border: 1px solid var(--border); border-radius: 8px; padding: 20px; }
  .project-title { font-size: 15px; font-weight: 700; margin-bottom: 8px; }
  .project-tags { font-size: 11px; color: var(--accent); letter-spacing: 0.3px; margin-bottom: 12px; text-transform: uppercase; font-weight: 600; }
  .project-desc { font-size: 13px; color: var(--text-secondary); margin-bottom: 14px; line-height: 1.55; }
  .project-link { font-size: 12px; font-weight: 600; color: var(--accent); text-decoration: none; }
  .project-link:hover { text-decoration: underline; }
  .project-private { font-size: 12px; color: #8a7f6a; font-style: italic; }

  /* Publications */
  .pub-item { padding: 14px 0; border-top: 1px solid var(--border); font-size: 14px; color: var(--text-secondary); }
  .pub-item:first-child { border-top: none; padding-top: 0; }
  .pub-item a { color: var(--text); font-weight: 600; text-decoration: none; border-bottom: 1px solid var(--accent); }
  .pub-item a:hover { color: var(--accent); }
  .pub-more { margin-top: 18px; font-size: 13px; }
  .pub-more a { color: var(--accent); font-weight: 600; text-decoration: none; }

  /* Contact / Footer */
  .contact-links { display: flex; flex-wrap: wrap; gap: 10px 24px; font-size: 14px; }
  .contact-links a { text-decoration: none; border-bottom: 1px solid var(--border); }
  .contact-links a:hover { color: var(--accent); border-color: var(--accent); }
  .footer-note { margin-top: 28px; font-size: 12px; color: var(--text-secondary); }

  @media (max-width: 640px) {
    .container { padding: 0 22px; }
    .hero h1 { font-size: 30px; }
    .hero-actions { flex-direction: column; }
    .btn { text-align: center; }
    .news-item { flex-direction: column; gap: 4px; }
    .news-date { flex: none; }
  }
</style>
</head>
<body>
<div class="container">

<section class="hero">
  <div class="hero-eyebrow">Wilmer Eye Institute · Baltimore</div>
  <h1>Luqman Munir</h1>
  <div class="hero-tagline">on retinas, research, and building things</div>
  <p class="hero-intro">Medical student researcher at Johns Hopkins Wilmer Eye Institute, working on ophthalmology AI, retinal imaging, and the software that supports both.</p>
  <div class="hero-actions">
    <a href="#projects" class="btn btn-solid">View Projects</a>
    <a href="assets/Luqman-Munir-CV.pdf" class="btn btn-outline">Download CV</a>
  </div>
</section>

<section class="section" id="news">
  <div class="section-label">News &amp; Updates</div>
  <div class="news-item">
    <div class="news-date">2025</div>
    <div class="news-text">Published "Retinal Laser Therapy Mechanisms, Innovations, and Clinical Applications" in <em>Photonics</em>.</div>
  </div>
  <div class="news-item">
    <div class="news-date">Sep 2025</div>
    <div class="news-text">Joined the Wilmer Glaucoma ML Lab (Dr. Yohanan) and the Wilmer Eye Research Institute (Dr. Fasika Woreta) as a visiting student.</div>
  </div>
  <div class="news-item">
    <div class="news-date">Jul 2025</div>
    <div class="news-text">Started as a Research Intern in the Paulus Lab, Retina Department.</div>
  </div>
</section>

</div>
</body>
</html>
```

- [ ] **Step 2: Verify the file is well-formed and the new content landed**

Run:
```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
grep -c "hero-tagline\|News &amp; Updates\|Paulus Lab, Retina Department" index.html
```
Expected: `3` (one match per grep alternative, i.e. all three strings present).

- [ ] **Step 3: Visually check in the browser**

Open `index.html` in the Browser tool, take a screenshot at desktop width, and confirm: cream background, serif "Luqman Munir" headline, italic terracotta tagline, two buttons, and a 3-row News list below with terracotta dates on the left. Then resize to a 375px-wide mobile viewport and confirm the buttons stack vertically and the news dates move above their text.

- [ ] **Step 4: Commit**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
git add index.html
git commit -m "feat: replace tools launcher with personal homepage — shell, hero, news"
```

---

### Task 2: About, In a Nutshell, and Research Experience sections

**Files:**
- Modify: `index.html` — insert new sections after the News & Updates `</section>` and before `</div>\n</body>`

**Interfaces:**
- Consumes: `.section`, `.section-label` classes and `.about-text`, `.nutshell-item`/`.nutshell-title`/`.nutshell-text`, `.exp-item`/`.exp-role`/`.exp-meta`/`.exp-focus`/`.exp-note` classes, all defined in Task 1's `<style>` block.
- Produces: the `id="about"`, `id="nutshell"`, `id="experience"` anchors (not consumed by any later task, but keep them — they match the spec's section list and are useful anchors).

- [ ] **Step 1: Insert the three sections**

In `index.html`, find this exact text (the end of the News & Updates section):

```html
  <div class="news-item">
    <div class="news-date">Jul 2025</div>
    <div class="news-text">Started as a Research Intern in the Paulus Lab, Retina Department.</div>
  </div>
</section>

</div>
</body>
</html>
```

Replace it with:

```html
  <div class="news-item">
    <div class="news-date">Jul 2025</div>
    <div class="news-text">Started as a Research Intern in the Paulus Lab, Retina Department.</div>
  </div>
</section>

<section class="section" id="about">
  <div class="section-label">About</div>
  <p class="about-text">I'm a medical student researching ophthalmology AI and retinal imaging at Johns Hopkins Wilmer Eye Institute. My work spans deep learning models for retinal disease, large-scale clinical database analysis, and the software infrastructure that keeps a research lab running. Outside the lab, I've published 21 peer-reviewed articles on population health and evidence-based clinical care.</p>
</section>

<section class="section" id="nutshell">
  <div class="section-label">In a Nutshell: What I'm Doing</div>
  <div class="nutshell-item">
    <div class="nutshell-title">Retinal Disease AI</div>
    <p class="nutshell-text">Building deep learning models — segmentation and biomarker prediction — and risk calculators for retinal detachment and AMD at the Paulus Lab.</p>
  </div>
  <div class="nutshell-item">
    <div class="nutshell-title">Research Infrastructure</div>
    <p class="nutshell-text">Designing and deploying the lab's project/task management dashboard, used lab-wide.</p>
  </div>
  <div class="nutshell-item">
    <div class="nutshell-title">Glaucoma Surgical Outcomes</div>
    <p class="nutshell-text">Studying IOP control strategies and surgical technique comparisons with the Wilmer Glaucoma ML Lab (Dr. Yohanan).</p>
  </div>
  <div class="nutshell-item">
    <div class="nutshell-title">Clinical Data &amp; Epidemiology</div>
    <p class="nutshell-text">Open globe injury outcomes and cataract curriculum research with Dr. Woreta's lab, paired with Epic EHR data extraction pipelines (SQL, Python) supporting it.</p>
  </div>
</section>

<section class="section" id="experience">
  <div class="section-label">Research Experience</div>
  <div class="exp-item">
    <div class="exp-role">Research Intern, Paulus Lab, Retina Department</div>
    <div class="exp-meta">Johns Hopkins Wilmer Eye Institute · Jul 2025 – present</div>
    <div class="exp-focus">Retinal disease AI, database-driven clinical research, and lab research infrastructure.</div>
  </div>
  <div class="exp-item">
    <div class="exp-role">Visiting Student, Wilmer Glaucoma ML Lab (Dr. Yohanan)</div>
    <div class="exp-meta">Johns Hopkins Wilmer Eye Institute · Sep 2025 – present</div>
    <div class="exp-focus">IOP prediction and surgical outcome comparisons for glaucoma.</div>
  </div>
  <div class="exp-item">
    <div class="exp-role">Visiting Student, Wilmer Eye Research Institute (Dr. Fasika Woreta)</div>
    <div class="exp-meta">Johns Hopkins Wilmer Eye Institute · Sep 2025 – present</div>
    <div class="exp-focus">Open globe injury outcomes, cataract curriculum research, and EHR data extraction.</div>
  </div>
  <p class="exp-note">Full role-by-role detail, certifications, and presentations are in the <a href="assets/Luqman-Munir-CV.pdf">full CV</a>.</p>
</section>

</div>
</body>
</html>
```

- [ ] **Step 2: Verify**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
grep -c "In a Nutshell: What I'm Doing\|Glaucoma Surgical Outcomes\|Visiting Student, Wilmer Eye Research Institute" index.html
```
Expected: `3`.

- [ ] **Step 3: Visually check in the browser**

Reload `index.html` in the Browser tool. Scroll past News & Updates and confirm: a one-paragraph About section, then four "In a Nutshell" blocks each with its own serif mini-heading and a hairline divider between them (not one flowing paragraph), then a Research Experience list with three roles, each showing role/institution/dates/focus, ending with a "full CV" link.

- [ ] **Step 4: Commit**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
git add index.html
git commit -m "feat: add About, In a Nutshell, and Research Experience sections"
```

---

### Task 3: Projects and Selected Publications sections

**Files:**
- Modify: `index.html` — insert new sections after the Research Experience `</section>` and before `</div>\n</body>`

**Interfaces:**
- Consumes: `.projects-grid`/`.project-card`/`.project-title`/`.project-tags`/`.project-desc`/`.project-link`/`.project-private` and `.pub-item`/`.pub-more` classes from Task 1's `<style>` block.

- [ ] **Step 1: Insert the two sections**

In `index.html`, find this exact text (the end of the Research Experience section):

```html
  <p class="exp-note">Full role-by-role detail, certifications, and presentations are in the <a href="assets/Luqman-Munir-CV.pdf">full CV</a>.</p>
</section>

</div>
</body>
</html>
```

Replace it with:

```html
  <p class="exp-note">Full role-by-role detail, certifications, and presentations are in the <a href="assets/Luqman-Munir-CV.pdf">full CV</a>.</p>
</section>

<section class="section" id="projects">
  <div class="section-label">Projects</div>
  <div class="projects-grid">
    <div class="project-card">
      <div class="project-title">RDS Risk Calculator</div>
      <div class="project-tags">Python · scikit-learn · Web calculator</div>
      <p class="project-desc">Elastic-net regression model, with propensity-score-matched variable screening, predicting 180-day outcomes after RRD repair — deployed as a public web calculator.</p>
      <a href="rds-calculator.html" class="project-link">Open calculator →</a>
    </div>
    <div class="project-card">
      <div class="project-title">OCT Segmentation Pipeline</div>
      <div class="project-tags">PyTorch · SegFormer-B4 · MONAI Label</div>
      <p class="project-desc">Deep learning segmentation model with active learning, automatically segmenting retinal detachment biomarkers on OCT images.</p>
      <div class="project-private">Private research repository</div>
    </div>
    <div class="project-card">
      <div class="project-title">RD OCT Biomarker Model</div>
      <div class="project-tags">Python · Biomarker modeling</div>
      <p class="project-desc">Downstream model that takes the segmented biomarkers from the pipeline above and predicts surgical outcomes from them.</p>
      <div class="project-private">Private research repository</div>
    </div>
    <div class="project-card">
      <div class="project-title">AMD CDS Tool</div>
      <div class="project-tags">Web app · Clinical decision support</div>
      <p class="project-desc">Clinical decision support tool for age-related macular degeneration, built for use alongside the RDS Risk Calculator.</p>
      <a href="amd-tool.html" class="project-link">Open tool →</a>
    </div>
    <div class="project-card">
      <div class="project-title">Lab Research Dashboard</div>
      <div class="project-tags">Next.js · PostgreSQL · Prisma</div>
      <p class="project-desc">Full-stack project, task, conference, and resource management platform built and deployed for lab-wide use, including a mobile-optimized interface.</p>
      <div class="project-private">Private research repository</div>
    </div>
  </div>
</section>

<section class="section" id="publications">
  <div class="section-label">Selected Publications</div>
  <div class="pub-item">Xie X, Munir L, Paulus YM. <a href="https://doi.org/10.3390/photonics12111043" target="_blank" rel="noopener">Retinal Laser Therapy Mechanisms, Innovations, and Clinical Applications.</a> Photonics. 2025.</div>
  <div class="pub-item">Munir L, et al. Efficacy and safety of LipiFlow® in the treatment of dry eye disease due to Meibomian gland dysfunction: an updated meta-analysis of randomized controlled trials. Ocul Surf. 2024. <em>(In Press)</em></div>
  <div class="pub-item">Munir L, Chaudhary AJ, Ammar ur Rahman M, Khalid A, Ijaz A. <a href="https://doi.org/10.1681/ASN.0000000000000480" target="_blank" rel="noopener">Trend analysis of kidney stone-related mortality, 1999-2020.</a> J Am Soc Nephrol. 2024.</div>
  <div class="pub-more"><a href="https://scholar.google.com/citations?user=wp3qUZAAAAAJ&hl=en" target="_blank" rel="noopener">View all 21 publications on Google Scholar →</a></div>
</section>

</div>
</body>
</html>
```

- [ ] **Step 2: Verify**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
grep -c "RD OCT Biomarker Model\|Lab Research Dashboard\|View all 21 publications on Google Scholar" index.html
```
Expected: `3`.

Also confirm the two private-repo projects don't have stray links, and the two linked projects point to real files in this repo:
```bash
grep -c "Private research repository" index.html   # expect 3
ls rds-calculator.html amd-tool.html                # both must exist
```

- [ ] **Step 3: Visually check in the browser**

Reload in the Browser tool. Confirm a 5-card project grid (collapsing to fewer columns as the window narrows — check at both desktop and ~375px width), with "Open calculator →" and "Open tool →" links on the two linked cards and an italic "Private research repository" note on the other three. Below that, confirm the publications list shows three entries with the first and third titles underlined/linked, the second left as plain text with "(In Press)", and a "View all 21 publications on Google Scholar →" link at the bottom. Click the DOI links and the Scholar link to confirm they open the right pages in a new tab.

- [ ] **Step 4: Commit**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
git add index.html
git commit -m "feat: add Projects and Selected Publications sections"
```

---

### Task 4: Contact/Footer section, CV PDF export, and final verification

**Files:**
- Modify: `index.html` — insert the Contact section after Publications, before `</div>\n</body>`
- Create: `assets/Luqman-Munir-CV.pdf` (exported from the CV docx)

**Interfaces:**
- Consumes: `.contact-links`, `.footer-note` classes from Task 1. Consumes `assets/Luqman-Munir-CV.pdf`, which this task creates and which the Hero (Task 1) and Research Experience (Task 2) buttons/links already point to.

- [ ] **Step 1: Insert the Contact/Footer section**

In `index.html`, find this exact text (the end of the Selected Publications section):

```html
  <div class="pub-more"><a href="https://scholar.google.com/citations?user=wp3qUZAAAAAJ&hl=en" target="_blank" rel="noopener">View all 21 publications on Google Scholar →</a></div>
</section>

</div>
</body>
</html>
```

Replace it with:

```html
  <div class="pub-more"><a href="https://scholar.google.com/citations?user=wp3qUZAAAAAJ&hl=en" target="_blank" rel="noopener">View all 21 publications on Google Scholar →</a></div>
</section>

<section class="section" id="contact" style="border-bottom:none;">
  <div class="section-label">Contact</div>
  <div class="contact-links">
    <a href="mailto:lmunir2@jh.edu">lmunir2@jh.edu</a>
    <a href="https://github.com/lmunir1" target="_blank" rel="noopener">GitHub</a>
    <a href="https://scholar.google.com/citations?user=wp3qUZAAAAAJ&hl=en" target="_blank" rel="noopener">Google Scholar</a>
    <a href="assets/Luqman-Munir-CV.pdf">Download CV</a>
  </div>
  <p class="footer-note">© 2026 Luqman Munir</p>
</section>

</div>
</body>
</html>
```

- [ ] **Step 2: Export the CV to PDF and place it in `assets/`**

```bash
mkdir -p "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io/assets"
SKILL_DIR="/Users/luqmanmunir/Library/Application Support/Claude/local-agent-mode-sessions/skills-plugin/afcf39ec-bc10-4ff9-95e9-d296678b058b/86aef78e-0c5a-4523-a612-6ce615eb0635/skills/docx"
cd /tmp
cp "/Users/luqmanmunir/Desktop/Personal/Documents/CV/CURRICULUM VITAE.docx" "CURRICULUM VITAE.docx"
python3 "$SKILL_DIR/scripts/office/soffice.py" --headless --convert-to pdf "CURRICULUM VITAE.docx"
cp "CURRICULUM VITAE.pdf" "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io/assets/Luqman-Munir-CV.pdf"
```

(If the skill directory path above no longer exists because the docx skill was reloaded under a new session path, re-run `Skill: anthropic-skills:docx` first to get the current base directory, then substitute it into `SKILL_DIR`.)

- [ ] **Step 3: Verify the PDF exists and is a real PDF**

```bash
file "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io/assets/Luqman-Munir-CV.pdf"
```
Expected: output contains `PDF document`.

- [ ] **Step 4: Verify the Contact section landed**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
grep -c "mailto:lmunir2@jh.edu\|© 2026 Luqman Munir" index.html
```
Expected: `2`.

- [ ] **Step 5: Full-page browser verification**

Open `index.html` in the Browser tool at desktop width and:
- Scroll through the entire page top to bottom; confirm every section from Task 1–4 renders in order with no visual breaks or overlapping text.
- Click "Download CV" (hero button, exp-note link, and footer link) and confirm the PDF opens and shows the updated CV content (the Software and Data Infrastructure Projects section, the Dr. Yohanan entries, etc. from this session's earlier CV edits).
- Click "View Projects" and confirm it scrolls to the Projects section.
- Click the GitHub and Google Scholar footer links and confirm they open the correct external pages.

Then resize to a 375px-wide mobile viewport, scroll through the whole page again, and confirm nothing overflows horizontally and the project grid is a single column.

- [ ] **Step 6: Commit**

```bash
cd "/Users/luqmanmunir/Desktop/Projects/lmunir1.github.io"
git add index.html assets/Luqman-Munir-CV.pdf
git commit -m "feat: add Contact section and CV PDF, complete personal homepage"
```
