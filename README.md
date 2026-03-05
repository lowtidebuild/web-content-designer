# Web Content Designer

A Claude skill that transforms raw text, articles, or URLs into polished, production-grade single-file HTML pages — complete with interactive navigation, Chart.js data visualizations, responsive layouts, and auto-selected design themes.

![Claude Skill](https://img.shields.io/badge/Claude-Skill-blueviolet?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Layouts](https://img.shields.io/badge/layouts-3-blue?style=flat-square)
![Themes](https://img.shields.io/badge/themes-10-orange?style=flat-square)

---

## What It Does

Give Claude any text content — a research paper, news article, meeting notes, financial analysis — and this skill turns it into a professional HTML presentation. No design skills required. The output is a single `.html` file you can open in any browser, host on any server, or embed anywhere.

### Three Layout Options

| Layout | Best For | Key Features |
|:--|:--|:--|
| **Interactive Dashboard** | Dense analytical content, reports with 5+ sections | Fixed sidebar nav, scroll-spy, sectioned panels, KPI cards |
| **Visual Infographic** | Narrative-driven content, storytelling, long-form analysis | Long-scroll flow, timelines, expert quotes, scenario cards, risk meters |
| **One-Page Executive Summary** | Quick briefings, TL;DR overviews | Single viewport (no scroll), 4 KPIs, bar chart, key points |

### 10 Auto-Selected Design Themes

The skill analyzes the content's subject matter and automatically applies the most fitting design system:

| Theme | Triggered By |
|:--|:--|
| Professional Blue | Corporate, finance, strategy, economics |
| Futuristic Tech | Technology, AI, innovation, space |
| Vibrant Creative | Culture, arts, society, education |
| Urgent Alert | Crisis, risk, conflict, warnings |
| Earthy Green | Environment, sustainability, wellness |
| Elegant Noir | Luxury, fashion, premium brands |
| Classic Academia | Academic, legal, historical research |
| Creative Pop | Startups, marketing, youth-oriented |
| Monochrome Minimal | Architecture, design, minimalism |
| Data-Driven Teal | Data analytics, statistics, dashboards |

---

## Installation

### Claude.ai (Recommended)

Download the `.zip` file from [Releases](../../releases) and upload it as a custom skill in your Claude.ai settings.

### Manual Setup

Clone this repo and place the `web-content-designer/` folder in your Claude skills directory:

```bash
git clone https://github.com/lowtidebuild/web-content-designer.git
```

---

## Usage

Simply ask Claude to visualize your content:

```
Make this into a dashboard:
[paste your article or text here]
```

```
이 텍스트를 인포그래픽으로 만들어줘:
[텍스트 붙여넣기]
```

```
Create a one-page executive summary from this report.
```

You can also provide a URL:

```
Turn this article into a visual infographic: https://example.com/article
```

### Trigger Phrases

The skill activates on phrases like:

- "make this into a dashboard / infographic / report"
- "visualize this article"
- "create an HTML report from this"
- "대시보드로 만들어줘"
- "인포그래픽으로 정리해줘"
- "요약 보고서 만들어줘"
- "이 텍스트를 시각화해줘"

---

## Examples

The `examples/` folder contains three real output samples — one for each layout:

| File | Layout | Theme | Description |
|:--|:--|:--|:--|
| `dashboard-example.html` | Interactive Dashboard | Professional Blue | U.S. Supreme Court IEEPA tariff ruling analysis |
| `infographic-example.html` | Visual Infographic | Urgent Alert | Iran-US conflict deep dive with timelines and scenario analysis |
| `summary-example.html` | One-Page Summary | Earthy Green | Global renewable energy outlook 2026 |

Open any of these `.html` files in your browser to see the expected output quality.

---

## Skill Architecture

```
web-content-designer/
├── SKILL.md                              # Main entry point (read first)
├── references/
│   ├── design-themes.md                  # 10-theme color matrix + application guide
│   ├── dashboard-structure.md            # Layout 1 blueprint: sidebar, scroll-spy, KPIs
│   ├── infographic-structure.md          # Layout 2 blueprint: long-scroll narrative
│   └── summary-structure.md             # Layout 3 blueprint: single-viewport, no-scroll
└── examples/
    ├── dashboard-example.html            # Real output sample (Layout 1)
    ├── infographic-example.html          # Real output sample (Layout 2)
    └── summary-example.html             # Real output sample (Layout 3)
```

**Progressive disclosure**: Claude reads only `SKILL.md` on trigger (~190 lines), then loads the relevant layout reference + example on demand. This keeps token usage efficient while maintaining high output quality.

---

## Technical Stack

Every generated HTML file is self-contained and uses:

- **[Tailwind CSS](https://tailwindcss.com/)** — Utility-first styling via CDN
- **[Chart.js](https://www.chartjs.org/)** — Interactive data visualizations
- **[Paperlogy Font](https://fonts-archive.github.io/Paperlogy/)** — Clean Korean/English typography
- **Vanilla JavaScript** — Scroll-spy, mobile menu, chart initialization

No build tools, no dependencies, no framework — just open the `.html` file in a browser.

---

## Compatibility

- **Claude models**: Claude Opus 4, Claude Sonnet 4, Claude Haiku 4 and above
- **Platforms**: Claude.ai, Claude Code, any environment with Claude skill support
- **Language support**: Korean and English (auto-detected from source content)
- **Browser support**: All modern browsers (Chrome, Firefox, Safari, Edge)

---

## Contributing

Contributions are welcome. Some areas that would be especially valuable:

- Additional layout templates (e.g., comparison report, timeline-focused)
- New design themes for underserved domains
- Localization support for additional languages
- Accessibility improvements (ARIA labels, keyboard navigation)

---

## License

MIT
