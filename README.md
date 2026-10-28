# AsaTechID Tools Hub — WordPress package

A responsive, shadcn/ui-inspired tools directory for AsaTechID. It uses plain HTML, scoped CSS, and vanilla JavaScript so it does not require a build step, npm, or a third-party library.

## Included tools

1. CCTV Storage Calculator
2. RAID Calculator
3. IPv4 Subnet Calculator
4. Bandwidth Calculator
5. Backup Storage Planner
6. PoE Power Calculator
7. Server Needs Calculator
8. UPS Backup Time Calculator
9. Wi-Fi Access Point Calculator
10. Rack Space Calculator
11. Storage Growth Planner
12. IT Requirements Generator

The UI includes search, category filters, responsive tool cards, modal calculators, input validation, result summaries, copy-result, and download-as-TXT actions.

## Quick install: WordPress Custom HTML block

1. Back up the page or create a draft first.
2. Open the page where the Tools Hub should appear.
3. Add a **Custom HTML** block (Gutenberg) or an HTML/code element supported by your page builder.
4. Open `wordpress-custom-html.html` in a text editor.
5. Copy the entire file contents into the Custom HTML block.
6. Replace `https://asatechid.com/contact/` with the correct contact URL if needed.
7. Preview desktop and mobile, test each calculator, then publish.

### Important WordPress script note

Some WordPress setups remove `<script>` tags from page content for users without the `unfiltered_html` capability, or a security plugin/page builder may block inline JavaScript. If the page appears but the tools do not open/calculate:

- Keep the HTML markup in the Custom HTML block.
- Put the CSS from the `<style>...</style>` section in **Appearance → Customize → Additional CSS** (or the theme's custom CSS panel), removing the opening/closing `<style>` tags.
- Put the JavaScript from the `<script>...</script>` section into a trusted snippets plugin's frontend JavaScript area, or enqueue it via a child theme. Do not paste executable JavaScript into a CSS field.
- If using a snippets plugin, set it to run on the public front end and only on the page containing this hub when possible.

Some page builders have their own HTML widgets and script execution rules; check the builder documentation for your installation.

## Customization

- **Brand / colors:** CSS variables are near the start of the stylesheet under `#asatechid-tools.ati`. The current design uses white surfaces, neutral borders, dark text, and restrained blue accents inspired by shadcn/ui patterns.
- **Contact link:** search for `https://asatechid.com/contact/`.
- **Language:** the widget is bilingual (Indonesian/English). Use the `ID` / `EN` pill in the top-right corner of the widget; the choice is stored in `localStorage` and remembered on the next visit. The initial language follows the browser locale. To add another language, add a new dictionary to the `I` object and a matching key on each tool `title`, `desc`, field `label`, `unit`, and `help` entry.
- **Simple / Advanced inputs:** every calculator opens in **Simple** mode with only the essential fields. Use the `Simple` / `Advanced` switch at the top of a calculator to reveal the extra options (reserve, efficiency, per-device U height, etc.). Fields marked `adv:true` in the `definitions` object are hidden in Simple mode; the switch choice is remembered in `localStorage` (`ati_mode`).
- **Categories:** tool card categories use `data-category` values: `storage`, `networking`, `infrastructure`, `planning`.
- **Tool calculations:** each tool is defined in the `definitions` object in the JavaScript. Review formulas and assumptions before using outputs for a real deployment.
- **Brand logo:** the letter “A” mark is a CSS text mark, not an official logo asset. Replace it with your official logo if available.

## Calculation caveats

These are planning estimates, not certified engineering designs:

- CCTV storage uses decimal TB and average bitrate; actual storage depends on recorder overhead, variable bitrate, audio, recording mode, RAID and manufacturer formatting.
- RAID formulas are theoretical for equal-sized disks. RAID 1 is modeled as a two-way mirror. RAID is not a backup.
- IPv4 subnet calculations show ordinary host ranges but call out `/31` and `/32` conventions.
- Bandwidth depends on actual traffic mix and peak concurrency.
- Backup estimate is simplified; it does not model deduplication, compression, synthetic full backups or all backup software behavior.
- PoE must be checked against both per-port limits and the switch's total PoE budget.
- Server estimator is a first-pass workload sum, not a substitute for measured utilization and vendor sizing.
- UPS runtime is approximate; use the exact UPS model's official runtime curve for final decisions.
- Wi-Fi AP estimator is a rough starting point and does not replace a site survey.
- Rack calculator does not model airflow, cable management or access requirements.
- Storage growth assumes a constant compounded monthly growth rate.
- IT requirements generator creates a general checklist, not a final bill of materials.

## SEO notes

This is an interactive widget package, not a complete SEO strategy by itself. For organic search:
- Create a dedicated indexable WordPress page at `/tools/` with a unique title, meta description, useful introductory text, and internal links.
- For high-priority tools, consider creating dedicated WordPress pages with unique explanatory content, FAQs, examples, formula explanations, and links to related articles.
- Avoid creating thin doorway pages that only repeat the same widget.
- Keep page titles, canonical URLs, breadcrumbs, and sitemap settings correct through your SEO plugin.
- Measure search impressions/clicks and tool engagement using Search Console and your analytics setup.
- Do not promise specific ranking improvements based on the widget alone.

## Browser support

Uses modern browser features, with clipboard fallback. The clipboard API can require HTTPS. The calculator itself runs locally in the visitor's browser and does not send entered values to a server.

## Files

- `wordpress-custom-html.html` — complete single-file fragment for a WordPress Custom HTML block (bilingual ID/EN).
- `index.html` — standalone bilingual page version (with `<!doctype>`, `<head>`, and `<body>`) for previewing in a browser.
- `README.md` — installation, customization, and caveats.
- `LICENSE.txt` — usage terms for this custom package.
