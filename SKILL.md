# Infographic Structure Reference (Layout 2)

The Visual Infographic is a **long-scroll narrative report** with rich visual storytelling. 
It reads like a premium editorial piece — flowing from top to bottom with embedded charts, 
data callouts, expert quotes, timelines, and comparison tables.

## Page Architecture

```
┌──────────────────────────────────────────────┐
│  Fixed Top Nav (horizontal, scrollspy)       │
├──────────────────────────────────────────────┤
│                                              │
│  Hero Section (full-width title + subtitle)  │
│                                              │
├──────────────────────────────────────────────┤
│  Section Bridge (transition text)            │
├──────────────────────────────────────────────┤
│  KPI Cards Row                               │
│  [KPI] [KPI] [KPI] [KPI]                    │
├──────────────────────────────────────────────┤
│  Section Bridge                              │
├──────────────────────────────────────────────┤
│  Content Block: Prose + Chart Side-by-Side   │
│  ┌────────────────┐ ┌────────────────────┐   │
│  │ Analysis text   │ │ Chart.js visual    │   │
│  └────────────────┘ └────────────────────┘   │
├──────────────────────────────────────────────┤
│  Timeline / Process Flow                     │
├──────────────────────────────────────────────┤
│  Expert Quotes / Insight Boxes               │
├──────────────────────────────────────────────┤
│  Comparison Table                            │
├──────────────────────────────────────────────┤
│  Strategy Cards Grid                         │
├──────────────────────────────────────────────┤
│  Scenario Analysis                           │
├──────────────────────────────────────────────┤
│  Final Recommendations / CTA                 │
└──────────────────────────────────────────────┘
```

## Two Navigation Variants

### Variant A: Fixed Sidebar (like the Dashboard but with infographic content flow)

Uses the same sidebar structure as Layout 1, but the main content area flows as a 
continuous narrative rather than discrete dashboard panels. Best for **8+ sections** 
with dense analytical content.

### Variant B: Fixed Top Navigation Bar

A horizontal nav bar fixed at the top. Better for **5-7 sections** with a more 
editorial, story-driven flow.

```html
<nav class="fixed top-0 left-0 right-0 bg-white/95 backdrop-blur-sm z-50 border-b shadow-sm">
    <div class="max-w-7xl mx-auto px-4 flex items-center justify-between h-16">
        <h1 class="text-lg font-bold text-primary truncate">Report Title</h1>
        <div class="hidden md:flex space-x-1" id="main-nav">
            <a href="#s1" class="nav-link px-3 py-1.5 rounded-lg text-sm font-medium">Section 1</a>
            <a href="#s2" class="nav-link px-3 py-1.5 rounded-lg text-sm font-medium">Section 2</a>
            <!-- ... -->
        </div>
        <button id="mobile-menu-button" class="md:hidden p-2"><!-- hamburger --></button>
    </div>
</nav>
<main class="pt-20 px-4 sm:px-8 lg:px-12 pb-24 max-w-5xl mx-auto">
    <!-- content flows here -->
</main>
```

**Choose the variant** based on content density: sidebar for comprehensive reports 
(the Iran-US war analysis, court ruling analysis type), top nav for more focused pieces.

## Key Visual Components

### 1. Hero Section

A bold opening that sets the stage:

```html
<section id="overview" class="content-section mb-16">
    <div class="inline-block px-3 py-1 bg-primary/10 text-primary font-bold text-sm 
                rounded-full mb-4">SECTION 1 — OVERVIEW</div>
    <h2 class="text-4xl md:text-5xl font-black mb-6 tracking-tight">
        Bold Headline That<br>Captures Attention
    </h2>
    <p class="text-lg md:text-xl leading-relaxed text-gray-700 mb-6 max-w-4xl">
        Opening paragraph that summarizes the situation...
    </p>
</section>
```

### 2. Section Bridges

Transitional elements between major sections that guide the reader:

```html
<div class="section-bridge bg-gray-50 border-l-3 border-primary p-4 rounded-r-lg mb-8">
    <p class="text-sm font-medium text-gray-700">
        <strong>Why does this matter?</strong> The following section examines...
    </p>
</div>
```

### 3. KPI Cards with Hover Effects

```html
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6 mb-12">
    <div class="kpi-card bg-white rounded-xl p-6 border border-primary/20 shadow-sm 
                hover:shadow-md hover:-translate-y-1 transition-all duration-300">
        <div class="text-3xl mb-2">⚡</div>
        <div class="text-3xl font-bold text-primary">145%</div>
        <div class="text-sm text-gray-600 mt-2">Year-over-year growth</div>
    </div>
</div>
```

### 4. Timeline Component

For chronological events or process flows:

```html
<div class="timeline-container relative pl-8">
    <!-- Vertical line -->
    <div class="absolute left-2 top-0 bottom-0 w-0.5 bg-primary/30"></div>
    
    <div class="timeline-item relative mb-8">
        <!-- Dot -->
        <div class="absolute -left-6 top-1 w-4 h-4 rounded-full bg-primary 
                     border-3 border-white shadow"></div>
        <div class="bg-white rounded-lg p-4 border border-gray-200 shadow-sm">
            <div class="text-xs font-bold text-primary mb-1">February 28, 2026</div>
            <h4 class="font-bold text-gray-900 mb-1">Event Title</h4>
            <p class="text-sm text-gray-600">Event description...</p>
        </div>
    </div>
    <!-- ... more timeline items -->
</div>
```

### 5. Expert Quote / Insight Box

```html
<div class="expert-quote border-l-4 border-primary bg-gradient-to-r from-primary/5 
            to-transparent p-5 rounded-r-lg my-6">
    <p class="text-gray-700 italic leading-relaxed">
        "Quoted analysis or key insight from the source..."
    </p>
    <p class="text-sm font-bold text-primary mt-2">— Source Attribution</p>
</div>
```

### 6. Side-by-Side Analysis (Prose + Chart)

```html
<div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-10">
    <div class="prose max-w-none text-gray-700 leading-relaxed">
        <p>Analysis text that explains the data shown in the chart...</p>
    </div>
    <div class="bg-white p-5 rounded-lg border border-gray-200 shadow-sm">
        <h4 class="font-bold mb-4 text-center">Chart Title</h4>
        <div class="relative h-72">
            <canvas id="chartId"></canvas>
        </div>
    </div>
</div>
```

### 7. Comparison / Data Table

```html
<div class="overflow-x-auto rounded-lg border border-gray-200 shadow-sm">
    <table class="w-full text-sm">
        <thead>
            <tr class="bg-gray-900 text-white">
                <th class="px-4 py-3 text-left font-bold uppercase tracking-wider text-xs">Column A</th>
                <th class="px-4 py-3 text-left font-bold uppercase tracking-wider text-xs">Column B</th>
            </tr>
        </thead>
        <tbody>
            <tr class="hover:bg-primary/5 transition-colors">
                <td class="px-4 py-3 border-b border-gray-100">Data</td>
                <td class="px-4 py-3 border-b border-gray-100">Data</td>
            </tr>
        </tbody>
    </table>
</div>
```

### 8. Strategy / Scenario Cards

```html
<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
    <div class="strategy-card bg-white border border-gray-200 rounded-xl p-6 
                hover:border-primary/50 hover:shadow-lg transition-all duration-300">
        <div class="text-2xl mb-3">🎯</div>
        <h4 class="font-bold text-lg mb-2">Strategy Title</h4>
        <p class="text-sm text-gray-600 leading-relaxed">Description...</p>
    </div>
</div>
```

### 9. Risk Meter / Progress Bars

```html
<div class="space-y-4">
    <div>
        <div class="flex justify-between text-sm mb-1">
            <span class="font-medium">Risk Factor A</span>
            <span class="text-primary font-bold">85%</span>
        </div>
        <div class="h-2 bg-gray-200 rounded-full overflow-hidden">
            <div class="h-full bg-primary rounded-full" style="width: 85%"></div>
        </div>
    </div>
</div>
```

## Narrative Flow Guidelines

The infographic layout is fundamentally about **storytelling**. Each section should 
connect to the next with intentional transitions:

1. **Open with the "what"** — What happened? What's the situation?
2. **Explain the "why"** — Root causes, background, contributing factors
3. **Show the "how"** — Mechanisms, processes, timelines
4. **Present the evidence** — Data, expert analysis, comparisons
5. **Assess the impact** — Who is affected? How severely?
6. **Close with the "so what"** — Recommendations, scenarios, calls to action

Use **section bridges** between major parts to maintain narrative momentum. 
The reader should feel like they're being guided through a story, not browsing 
disconnected panels.

## Section Numbering

Use numbered section labels for navigation clarity:

```html
<span class="section-number inline-flex items-center justify-center w-7 h-7 
             bg-primary text-white rounded-full text-xs font-bold mr-2">1</span>
```

This helps readers orient themselves in long-scroll content and provides visual 
anchoring in the navigation sidebar/bar.
