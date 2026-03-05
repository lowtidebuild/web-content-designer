# One-Page Executive Summary Structure Reference (Layout 3)

The One-Page Summary is a **compact, single-viewport overview** designed to fit on 
one screen without scrolling. Think of it as a strategic consultant's briefing slide — 
dense with information but visually clean.

## Critical Constraint

**NO SCROLLBARS.** The entire report must fit within a single viewport (approximately 
100vh). This means:
- Every text element must be aggressively condensed
- No component may overflow its container
- No internal scrollbars on any element
- Content that doesn't fit must be cut — not squeezed

This constraint is the defining characteristic of Layout 3. If in doubt, **remove 
content rather than let it overflow.**

## Page Architecture

```
┌───────────────────────────────────────────────────────┐
│  HEADER: Title + Subtitle + Date                      │
├───────────────────────────────────────────────────────┤
│  EXECUTIVE SUMMARY (2-3 lines max)                    │
├───────────┬───────────┬───────────┬───────────────────┤
│  KPI 1    │  KPI 2    │  KPI 3    │  KPI 4            │
├───────────┴───────────┴───────────┴───────────────────┤
│                       │                               │
│  KEY POINTS           │  DATA VISUALIZATION           │
│  (4 bullet items)     │  (bar chart or doughnut)      │
│                       │                               │
├───────────────────────┴───────────────────────────────┤
│  STRATEGIC RECOMMENDATION (1 sentence)                │
└───────────────────────────────────────────────────────┘
```

## Content Preparation (Before Coding)

You must restructure the source content into these exact slots. This is a **strategic 
summarization** exercise — not copy-paste.

### Slot 1: Main Title
The core topic in the fewest possible words. Maximum ~8 words.

### Slot 2: Executive Summary
The entire source condensed into 2-3 short sentences. This should answer: 
"What is this about and why does it matter?"

### Slot 3: KPIs (×4)
Find the 4 most impactful numbers from the source. Each KPI has:
- An emoji icon (1 character)
- A number + unit (e.g., "$29.6B", "6:3", "145%")
- A label of maximum ~8 words

**Strict rule**: The label must NOT exceed 2 short lines when rendered. 
If it's too long, rewrite it shorter.

### Slot 4: Data Visualization
Find 2-4 comparable data points and create a simple bar chart or doughnut chart. 
If no directly chartable data exists, create a representative chart from the 
source's main categories or comparisons.

### Slot 5: Key Points (×4)
Extract the 4 most important arguments or findings. Format each as:
```
<strong>Keyword:</strong> One-sentence explanation.
```

**Bad example** (too long):
> Physical album sales have been declining, making it strategically crucial 
> to diversify revenue streams through concerts, streaming, merchandise, and 
> other channels.

**Good example** (concise):
> <strong>Revenue diversification:</strong> Album sales declining; concerts, 
> streaming, and merch increasingly critical.

### Slot 6: Strategic Recommendation
One powerful, actionable sentence summarizing the source's ultimate conclusion 
or implication.

## HTML Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Executive Summary</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/fonts-archive/Paperlogy/subsets/Paperlogy-dynamic-subset.css" type="text/css"/>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html, body {
            height: 100vh;
            overflow: hidden; /* CRITICAL: prevents page scroll */
            font-family: "Paperlogy", -apple-system, BlinkMacSystemFont, "Segoe UI", 
                         Roboto, sans-serif;
            background-color: var(--bg);
            color: var(--text);
        }
        :root {
            --primary: #0052cc;
            --bg: #f0f2f5;
            --text: #172b4d;
            --accent: #e6f0ff;
        }
        .summary-grid {
            display: grid;
            grid-template-rows: auto auto auto 1fr auto;
            height: 100vh;
            padding: 1.5rem;
            gap: 1rem;
        }
        .kpi-row {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.75rem;
        }
        .kpi-card {
            background: white;
            border-radius: 0.75rem;
            padding: 1rem;
            text-align: center;
            border-top: 3px solid var(--primary);
            box-shadow: 0 1px 3px rgba(0,0,0,0.08);
        }
        .kpi-number {
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--primary);
        }
        .kpi-label {
            font-size: 0.7rem;
            color: #6b7280;
            margin-top: 0.25rem;
            line-height: 1.3;
        }
        .content-area {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
            min-height: 0; /* prevents grid blowout */
        }
        .card {
            background: white;
            border-radius: 0.75rem;
            padding: 1.25rem;
            box-shadow: 0 1px 3px rgba(0,0,0,0.08);
            overflow: hidden; /* CRITICAL: prevents content overflow */
        }
        .key-point {
            font-size: 0.8rem;
            line-height: 1.4;
            padding: 0.5rem 0;
            border-bottom: 1px solid #f3f4f6;
        }
        .key-point:last-child { border-bottom: none; }
        .footer-bar {
            background: var(--primary);
            color: white;
            padding: 0.75rem 1.25rem;
            border-radius: 0.75rem;
            font-size: 0.85rem;
            font-weight: 600;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="summary-grid">
        <!-- HEADER -->
        <div>
            <h1 style="font-size: 1.5rem; font-weight: 800; color: var(--primary);">
                {{MAIN_TITLE}}
            </h1>
            <p style="font-size: 0.75rem; color: #6b7280; margin-top: 0.25rem;">
                Date · Source Attribution
            </p>
        </div>

        <!-- EXECUTIVE SUMMARY -->
        <div class="card" style="padding: 1rem;">
            <p style="font-size: 0.85rem; line-height: 1.5;">
                {{EXECUTIVE_SUMMARY_2_TO_3_LINES}}
            </p>
        </div>

        <!-- KPI ROW -->
        <div class="kpi-row">
            <div class="kpi-card">
                <div>📊</div>
                <div class="kpi-number">{{VALUE}}</div>
                <div class="kpi-label">{{SHORT_LABEL}}</div>
            </div>
            <!-- repeat ×4 -->
        </div>

        <!-- CONTENT AREA: Key Points + Chart -->
        <div class="content-area">
            <div class="card">
                <h3 style="font-size: 0.9rem; font-weight: 700; margin-bottom: 0.75rem; 
                           color: var(--primary);">Key Points</h3>
                <div class="key-point">
                    <strong>Keyword:</strong> One-line summary.
                </div>
                <!-- repeat ×4 -->
            </div>
            <div class="card">
                <h3 style="font-size: 0.9rem; font-weight: 700; margin-bottom: 0.75rem; 
                           color: var(--primary);">Data Overview</h3>
                <div style="position: relative; height: calc(100% - 2rem);">
                    <canvas id="summaryChart"></canvas>
                </div>
            </div>
        </div>

        <!-- STRATEGIC RECOMMENDATION -->
        <div class="footer-bar">
            💡 {{ONE_SENTENCE_STRATEGIC_RECOMMENDATION}}
        </div>
    </div>

    <script>
    document.addEventListener('DOMContentLoaded', function() {
        const ctx = document.getElementById('summaryChart');
        if (ctx) {
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['A', 'B', 'C'],
                    datasets: [{
                        data: [30, 50, 20],
                        backgroundColor: [
                            'rgba(0, 82, 204, 0.8)',
                            'rgba(0, 82, 204, 0.6)',
                            'rgba(0, 82, 204, 0.4)'
                        ],
                        borderRadius: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { beginAtZero: true, ticks: { font: { size: 10 } } },
                        x: { ticks: { font: { size: 10 } } }
                    }
                }
            });
        }
    });
    </script>
</body>
</html>
```

## Final Verification Checklist

Before delivering the summary, verify:

1. **No scrollbars** — Open the HTML and confirm no scroll appears on a standard 
   1920×1080 viewport
2. **No overflow** — No text is clipped, hidden, or bleeding outside card boundaries
3. **No empty space** — Every component contains real content from the source
4. **No long text** — Every label, description, and bullet is aggressively concise
5. **Chart renders** — The Chart.js visualization loads and displays properly
6. **Theme applied** — All colors match the selected design theme
7. **Components don't overlap** — Each grid cell stays within its bounds

## Responsive Considerations

The one-page summary is primarily designed for desktop/laptop screens. On mobile:
- Stack the KPI cards 2×2 instead of 4×1
- Stack the content area vertically
- Allow scrolling on mobile only (keep `overflow: hidden` for desktop via media query)

```css
@media (max-width: 768px) {
    html, body { overflow: auto; height: auto; }
    .summary-grid { height: auto; }
    .kpi-row { grid-template-columns: repeat(2, 1fr); }
    .content-area { grid-template-columns: 1fr; }
}
```
