# Hunter Software Consulting website

A static Hugo site. Project-owned layouts and CSS provide the consulting presentation; the vendored themes remain unchanged. Production uses GitHub Pages and Hugo Extended 0.154.4.

## Local review

```sh
git submodule update --init --recursive
hugo --gc --minify
python3 scripts/check_site.py public
python3 scripts/preview.py --directory public --port 1318
```

Open http://127.0.0.1:1318/. Rebuild and refresh after changing source. The preview binds only to loopback, disables browser caching, and returns the site's custom page with HTTP 404 for unknown paths.

For live development, `hugo server --disableFastRender --port 1318` also works. Restart it after frontmatter changes if content appears misaligned; this occurred with the installed Hugo 0.155.2 during this review. Final QA used a clean production build served with the Python preview above.

## Editing

- Homepage copy: `content/_index.md`; composition: `layouts/home.html`.
- Services and experience: `content/pages/services.md`, `content/pages/about-me.md`.
- Homepage experience introduction and outcome examples: `data/experience.toml`, with links to the corresponding evidence on Experience.
- Engagement sequence: `data/engagement.toml`. The phase durations in the internal offer are planning guidance, not fixed public promises.
- Writing and existing recommendations: `content/posts/`, `content/testimonials/`.
- Navigation, contact destinations and organization metadata: `hugo.toml`.
- Layouts, structured data and metadata: `layouts/`; typography, palette and responsive behavior: `assets/css/site.css`.
- Brand source image: `static/images/hunter-logo.png`. The header uses the complete original artwork at its natural aspect ratio. Headshot source: `assets/images/hunter-harris.png`; Hugo generates responsive WebP copies.
- Typography: one self-hosted Archivo family, normal width, regular/semibold weights. Shared role tokens are at the end of `assets/css/site.css`; change those instead of adding page-specific font treatments. The font license is `static/fonts/archivo-OFL.txt`.

Keep published URLs and original publication dates stable. Add `lastmod` when the page changes meaningfully. Give each page a specific description and one H1; body headings start at H2. Keep consulting scope, employee work and advisory feedback distinct. Maintain the supporting evidence separately from the public repository.

## Homepage content updates

No monthly template redesign is required. Content changes become visible on the next build and publication through the existing GitHub Pages workflow.

- **Latest writing:** Hugo selects the three newest published posts by frontmatter `date`, newest first. Titles, dates, descriptions and links come from the posts. Drafts and future-dated posts are excluded by the existing build settings. No article IDs are maintained in the homepage template.
- **Newsletter/podcast:** `hugo.toml` supplies `newsletterURL` for the footer and Writing archive. The footer links the podcast only on YouTube.
- **Featured recommendation:** add `homepageFeatured = true` to the chosen testimonial's TOML frontmatter and remove that flag from the previous one. The homepage reads `excerpt`, `quoteAuthor`, `quoteRole` and `feedbackType` from that file. Keep the excerpt verbatim and its advising context accurate. If more than one is featured, the newest wins; with none featured, the newest recommendation is used.
- **Outcome examples:** edit `data/experience.toml` to change homepage highlights without editing the template. Each entry needs a supported business or customer change and a working link to its fuller account on Experience. Selection is editorial; the site does not infer results from new posts.
- **Engagement:** all five phase actions and intended outcomes are visible. Edit the `action` and `outcome` fields in `data/engagement.toml` once to update both the homepage sequence and Services. The existing phase names and order remain the offer's source-of-truth contract.
- **Evergreen copy:** positioning and page composition change when the offer or site strategy changes, not when a new post is published.

The content-to-homepage behavior was verified using a temporary content copy: adding a post, excluding a draft, changing an excerpt, and changing the selected recommendation all updated the next build without template edits.

Across pages, lead with the business result or enabled customer behavior, then explain the work behind it. Use the source/claim ledger to distinguish achieved changes from intended engagement outcomes. Do not turn a feature, release or advisory recommendation into an unsupported revenue, retention or adoption claim.

An outcome-sounding heading is not enough. Before selecting an experience example, identify the supported change in the customer's situation or the business's performance, then show the judgment that contributed. A new capability alone belongs in a description of scope; do not promote it into the site's proof merely by adding a benefit. Prefer fewer substantial examples to a feature-by-feature project inventory.

Hunter's September 18 clarification permits credible estimates drawn from his resume and first-person accounts; audited financial records are not a prerequisite. Preserve what a metric measures and its timeframe, and distinguish team results from sole attribution. His September 19 correction removes blanket disclaimers and repeated "about" wording: use direct, rounded figures without suggesting audited precision. Cross-check materially conflicting stories. External benchmarks may inform an explicitly modeled cost estimate; they do not establish a past employer's measured savings.

Hunter's September 19 direction removes the career-title list. Keep the company stories in reverse chronological order: Presage Technologies, Owner.com, Sendoso, Calendly, Salesloft, Silverpop. Presage is current; show Hunter's ownership of its emerging product organization, with the Brown research partnership as a customer-impact example. Show the customer problem, Hunter's judgment and ownership, and the result. Give distinct results their own subsections rather than burying them under "I also." Preserve old inbound anchors without restoring the visible career history.

Owner.com's $25M result is additional revenue from coupon-driven restaurant orders, not ARR or recurring revenue. Hunter explicitly corrected his own terminology in this task; that correction overrides the repeated ARR wording in older transcripts, resumes and positioning materials. Keep the correction consistent in page copy, homepage highlights, descriptions and generated metadata. The short implementation duration does not mean all the revenue arrived that afternoon.

Use the company name from Hunter's tenure, with a brief current-name note where helpful: Silverpop / IBM, now Acoustic. Link each company story to its official current website once in the prose; keep headings and the table of contents as internal navigation. Experience advising uses a few concise, sourced outcome summaries, each linking to its full existing testimonial. These are editorial selections, not monthly template work.

Experience and supporting homepage copy use Hunter's shared `website-proof-copy` writer/editor process. Future revisions should retain source evidence and a distinct editorial review before publication.

## Build checks and deployment

`scripts/check_site.py` checks generated links, anchors, metadata, heading structure, image alternative text, JSON-LD relationships, sitemap exclusions and contact destinations. It uses only Python's standard library. To compare a previous build, add `--baseline /path/to/previous/public`. JSON output is available with `--json /path/to/checks.json`.

`.github/workflows/hugo.yml` builds and validates on pushes to `main` and on manual dispatch, then deploys to GitHub Pages. The workflow's Pages base URL is authoritative during deployment.

Local review evidence, screenshots and private editorial receipts are excluded from the public repository.
