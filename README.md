# KPI Alignment Tool

A web dashboard that finds where different teams define the same business metric differently, so they can agree on one definition. Course project for a University of Washington class (579).

## The problem

Teams such as Marketing, Sales, Product, and Customer Success often use the same metric name (for example "conversion" or "retention") to mean different things. When leaders compare numbers across teams, they compare different measurements. This tool takes a list of team KPI definitions and shows where they conflict, overlap, or are too vague.

## What it does

On load, the app reads a table of KPIs with three columns (`Team`, `Metric_Name`, `Definition`) and analyzes it. Each tab shows a different view:

| Tab | What it shows |
| --- | --- |
| KPI Data | Searchable, filterable table of all definitions |
| Analysis | Per-metric summary, conflicts, how each team's wording translates, and a recommended definition |
| Conflicts | Definitions that are vague (no time frame, vague wording), overlapping (similar concepts), or incompatible (same name, different method) |
| Scenarios | Example situations showing how two teams could read the same metric differently |
| Funnel | Metrics grouped into Awareness, Consideration, Conversion, Retention, or Unknown, with a chart by team |
| Scorecard | A 0 to 100 alignment score for each team |
| Priority | Metrics ranked using adjustable team weights |
| Glossary | A standard name and definition for each metric |
| Translator | Rewrites a message from one team's KPI terms into another team's |
| Generator | Groups metrics into families and proposes a standard definition for each |

## How it works

All analysis is **rule-based, not machine learning and not an LLM**. Examples (see `lib/kpi-analyzer.ts` and `components/kpi-alignment-dashboard.tsx`):

- Metrics are grouped by lowercased name; a conflict is flagged when the same name has different definitions.
- A definition is "vague" if it has no number-plus-time-unit (such as "30 days"), uses words like "varies" or "multiple", or uses "or" without a threshold.
- Funnel stages are assigned by keywords in the metric name and definition (for example "churn" maps to Retention).
- The recommended definition is simply the longest one.
- Team scores start at 100 and lose points for overlaps and conflicts.

## Limitations

- The data is a sample CSV hosted on Vercel Blob, loaded when the page opens. There is no file upload, and the app shows an error if that file is unavailable.
- The CSV is split on commas, so a definition containing a comma inside quotes would be read incorrectly.
- Keyword rules are simple and will misclassify some metrics.
- The Export buttons in the Analysis and Glossary tabs only show a placeholder alert; nothing is exported.
- Scenario text is written from templates rather than generated from your data.

## Tech stack

Next.js 15, React 19, TypeScript, Tailwind CSS, shadcn/ui, Recharts, Chart.js.

## Run it locally

Requires Node.js 18.18 or newer and [pnpm](https://pnpm.io/).

```bash
git clone https://github.com/Eantan2/579-Assignment-1.git
cd 579-Assignment-1
pnpm install
pnpm dev
```

Then open http://localhost:3000.

## How it was built

The user interface was generated with Vercel's v0 AI tool, as the course required, and then deployed on Vercel. I specified the problem, the metrics and views to include, and the analysis rules, and reviewed the output. The commit history shows only the v0 sync because the tool commits the changes.

## Deployment

Your project is live at:

**[https://vercel.com/eantan2s-projects/v0-new-project-kt5zfv2qi9k](https://vercel.com/eantan2s-projects/v0-new-project-kt5zfv2qi9k)**

## Build your app

Continue building your app on:

**[https://v0.dev/chat/projects/KT5zfv2Qi9K](https://v0.dev/chat/projects/KT5zfv2Qi9K)**
