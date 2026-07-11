# Screenshots to capture for the portfolio

These are the shots that sell the workflow on Upwork. Capture them from the n8n editor at http://localhost:5678 after you import the workflow and run it once. Order matters: lead with the overview, then prove it runs, then show the detail that signals engineering judgment.

Set the browser zoom so sticky-note text is readable. Use the canvas zoom-to-fit control (bottom left) before the wide shots. Light mode reads better in a proposal than dark mode.

## 1. Canvas overview (the hero image)

- Open the workflow and click zoom-to-fit so the whole thing is in frame.
- All 6 sticky notes must be legible: the overview note at top, plus Queue, Failover, Normalize+SEO, Publish, and Log.
- This one image tells the whole story: schedule, queue, primary model, failover branch, SEO, publish, log.
- Filename suggestion: `01-canvas-overview.png`.

## 2. Failover branch close-up (the differentiator)

- Zoom into the three nodes: **Generate Article - Primary (Groq)**, **IF Primary Failed?**, and **Fallback - Gemini**.
- Include the red Failover sticky note so the reviewer reads why the branch exists.
- If you can, capture it right after a keyless run so the Groq node shows its failed state and the connector into Gemini is the active path.
- Filename suggestion: `02-failover-branch.png`.

## 3. Successful execution (proof it runs)

- Click **Execute Workflow** and wait for it to finish.
- Capture the canvas with the green check badges along the mock path: Schedule, Keyword Queue, Groq, IF, Gemini, Normalize, SEO, Publish (mock), Run Log.
- The green trail plus the item counts on each connector is the proof shot.
- Filename suggestion: `03-successful-run.png`.

## 4. Run Log output (the outcome record)

- After the run, click the **Run Log** node and open its output panel.
- Show the JSON summary: keyword, title, slug, focus_keyword, word_count, provider_used, demo_mode, status.
- This demonstrates observability, not just generation.
- Filename suggestion: `04-run-log-output.png`.

## 5. Credential-free auth detail (the trust signal)

- Open the **Generate Article - Primary (Groq)** node and show the Authorization header set to `Bearer {{ $env.GROQ_API_KEY }}`.
- This proves no secrets are hardcoded and that the workflow is safe to share.
- Filename suggestion: `05-env-auth.png`.

## 6. Publish detail (mock plus real target) — optional

- Frame the **Publish to WordPress (mock)** node next to the disabled **Publish to WordPress (real)** node and the Publish sticky note.
- Shows that the demo is runnable now and production-ready with one credential.
- Filename suggestion: `06-publish-mock-and-real.png`.

## Caption ideas for the listing

- "One workflow, two model providers, zero downtime when one fails."
- "Rebuilt the failover pattern from my production publisher (658+ posts, 41 days unattended) in n8n."
- "Runs end to end with no API keys. Add your own to go live."

## Where to use them

- Upwork portfolio item: lead with shot 1, then 3, then 2.
- Proposal attachments: 2 and 4 make the strongest case in a cover letter.
