# Recommendability Scorecard

Link to scorecard here: https://anastashaha.github.io/evaluationframework/

An interactive scoring tool for the Endangered Languages Project's **ethical technology evaluation framework** — a way to decide whether a language technology tool is safe to recommend to a community.

This has been built intentionally as a single static web page (`index.html`) so there is no build step, no server, and no dependencies beyond a Google Fonts stylesheet). Open it directly in a browser or host it anywhere that serves static files.

## What it does

The page walks through ten evaluation categories (need and fit, origin and consent, cultural protocols, data ownership, benefit-sharing, security and privacy, provider governance, AI/algorithmic use, disaster recovery, usability and maintenance). For each one you:

1. Expand **"Guiding questions"** to see the specific things to ask the provider or check yourself, and tick each one off as you confirm it.
2. Rate the category **Not met / Partial / Met** (0 / 1 / 2 points).
3. Optionally adjust its **weight** — categories default to ×3 (rights-defining), ×2 (risk-mitigating), or ×1 (practical), but any community can re-weight them to match its own priorities.

The right-hand panel recalculates live:

- **Weighted score and percentage** — weighted points ÷ (total weight × 2).
- **Hard gates, chosen by the community** — click the flag icon (⚐) next to any guiding question, in any category, to mark it non-negotiable. Flagged questions appear in the "Your community's hard gates" list in the summary panel, and the tool is not recommendable — a red banner overrides the numeric score — until every flagged question is checked off. There's no fixed list of gates baked in; each community picks the specific questions that represent a hard line for them (e.g. "Do we have real technical control to export and delete our data?"), and can unflag a question at any time with the × next to it in that list.

Ratings, weights, question checkmarks, and which questions are flagged as hard gates are all saved automatically to the browser's local storage, so progress survives a page reload. Nothing is sent anywhere — there's no backend and no analytics; all state lives only in the evaluator's own browser.

A **Save as PDF** button expands all guiding questions and opens the browser print dialog, producing a clean paper record for a written recommendation file.

## Running it locally

No build step is required. Either:

- Open `index.html` directly in a browser, or
- Serve the folder with any static file server, e.g.:

  ```
  python3 -m http.server 8000
  ```

  then visit `http://localhost:8000`.

## How to host this page

Everything the tool needs (the design, the questions, the scoring logic) lives inside the one file, `index.html`. There's nothing to install and nothing to configure.

### Option 1: Put it on its own link (fastest, no account needed)

1. Go to [app.netlify.com/drop](https://app.netlify.com/drop) in your browser.
2. Drag the `index.html` file into the page.
3. Netlify gives you a live link in a few seconds.

### Option 2: If you would like to add this as its own page in your website

How you do this depends on how your website is built — pick whichever matches:

**If your website lets you upload a page directly** (common in WordPress, Squarespace, Wix, and similar site builders):
1. Find the option to add a new page or upload an HTML file (usually under Pages or Media).
2. Upload `index.html`.
3. Add it to your site's menu so people can find it.

**If you want it to appear inside a page you already have** (surrounded by your normal site header, footer, etc.):
1. Host `index.html` somewhere first (Option 1 above works well for this).
2. On the page where it should appear, paste this, replacing `YOUR-LINK-HERE` with the link from step 1:
   ```html
   <iframe src="YOUR-LINK-HERE" style="width:100%; height:900px; border:none;"></iframe>
   ```

### Option 3: Use GitHub Pages (free, if you already use GitHub)

1. Create a new GitHub repository and upload `index.html` to it.
2. In the repository, go to **Settings → Pages**, and set it to publish from the `main` branch.
3. GitHub will give you a permanent link that looks like `https://your-username.github.io/your-repo-name`.

## Files

- `index.html` — the entire application (markup, styles, and scoring logic).

## Customizing

- **Categories and guiding questions** live in the `CATEGORIES` array near the top of the `<script>` block in `index.html`. Hard gates are not a separate list — they're just guiding questions a community has flagged at runtime, so adding or editing questions here is all that's needed.
- **Default tier weights** are set in the `TIERS` object (`rights: 3`, `risk: 2`, `practical: 1`).

Editing the `CATEGORIES` array is enough to retarget the tool for a different checklist — the scoring, layout, and print behavior all adapt automatically.
