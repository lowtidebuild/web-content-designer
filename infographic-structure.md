# Dashboard Structure Reference (Layout 1)

The Interactive Dashboard uses a **fixed sidebar navigation** with scrollable main content. 
The sidebar remains visible at all times on desktop, providing instant access to any section.

## Page Architecture

```
┌──────────────────────────────────────────────┐
│ ┌──────────┐ ┌─────────────────────────────┐ │
│ │          │ │  Sticky Header Bar          │ │
│ │ SIDEBAR  │ ├─────────────────────────────┤ │
│ │ (fixed)  │ │                             │ │
│ │          │ │  Hero / Summary Banner      │ │
│ │ • Nav 1  │ │                             │ │
│ │ • Nav 2  │ ├─────────────────────────────┤ │
│ │ • Nav 3  │ │                             │ │
│ │ • Nav 4  │ │  KPI Cards Row              │ │
│ │ • Nav 5  │ │  [KPI] [KPI] [KPI] [KPI]   │ │
│ │          │ ├─────────────────────────────┤ │
│ │          │ │                             │ │
│ │          │ │  Content Section 1          │ │
│ │          │ │  (charts, tables, prose)    │ │
│ │          │ │                             │ │
│ │          │ ├─────────────────────────────┤ │
│ │          │ │  Content Section 2          │ │
│ │          │ │  ...                        │ │
│ └──────────┘ └─────────────────────────────┘ │
└──────────────────────────────────────────────┘
```

## HTML Structure

```html
<body class="flex h-screen overflow-hidden">

    <!-- Mobile Menu Button (visible on small screens) -->
    <div class="md:hidden fixed top-4 left-4 z-50">
        <button id="mobile-menu-button" class="p-2 bg-primary text-white rounded-md shadow-md">
            <!-- hamburger icon SVG -->
        </button>
    </div>

    <!-- Fixed Sidebar Navigation -->
    <nav id="sidebar" class="bg-primary text-white w-72 flex-shrink-0 h-full overflow-y-auto 
         transform -translate-x-full md:translate-x-0 transition-transform duration-300 
         fixed md:relative z-40 shadow-xl">
        <div class="p-6">
            <h1 class="text-2xl font-bold mb-8 leading-tight">
                Title<br>
                <span class="text-sm font-normal opacity-80">Subtitle</span>
            </h1>
            <ul id="main-nav" class="space-y-2">
                <li><a href="#section1" class="sidebar-link block py-3 px-4 rounded active">Section 1</a></li>
                <li><a href="#section2" class="sidebar-link block py-3 px-4 rounded">Section 2</a></li>
                <!-- ... more nav items -->
            </ul>
        </div>
    </nav>

    <!-- Scrollable Main Content -->
    <main class="flex-1 h-full overflow-y-auto relative scroll-smooth">
        <!-- Sticky Header -->
        <header class="bg-white shadow-sm sticky top-0 z-10">
            <div class="px-6 py-4 flex justify-between items-center ml-12 md:ml-0">
                <h2 class="text-xl font-bold">Page Title</h2>
                <span class="text-sm text-gray-500">Source attribution</span>
            </div>
        </header>

        <!-- Content Container -->
        <div class="p-6 space-y-10 max-w-7xl mx-auto pb-12">
            <!-- Hero Banner -->
            <!-- KPI Cards -->
            <!-- Content Sections -->
        </div>
    </main>
</body>
```

## Key Components

### 1. Sidebar Navigation

The sidebar is the defining feature of this layout. It must:
- Stay **fixed** on desktop (always visible while content scrolls)
- **Collapse off-screen** on mobile with a hamburger toggle
- Show an **active state** on the current section (scroll-spy)
- Use the theme's `Primary` color as its background

**Active state CSS:**
```css
.sidebar-link.active {
    background-color: rgba(255, 255, 255, 0.2);
    border-left: 4px solid #ffffff;
    font-weight: bold;
}
```

### 2. Hero / Summary Banner

A colored banner below the header that gives a 2-3 sentence overview of the entire 
content. Often includes:
- An icon (SVG inline)
- Source attribution or methodology note
- Key links or references

```html
<div class="bg-accent border-l-4 border-primary p-5 rounded-lg shadow-sm">
    <h3 class="font-bold text-lg flex items-center">
        <!-- icon --> Title
    </h3>
    <p class="text-sm mt-2 leading-relaxed">Brief overview...</p>
</div>
```

### 3. KPI Cards Row

A responsive grid of 3-4 key metrics extracted from the source content:

```html
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
    <div class="kpi-card bg-white rounded-lg p-5 border-l-4 border-primary shadow-sm">
        <div class="text-3xl mb-1">📊</div>
        <div class="text-2xl font-bold text-primary">$29.6B</div>
        <div class="text-sm text-gray-600 mt-1">Global market size (2024)</div>
    </div>
    <!-- ... more KPI cards -->
</div>
```

### 4. Content Sections

Each section corresponds to a sidebar nav item. Structure:

```html
<section id="section1" class="content-section bg-white p-6 md:p-8 rounded-xl shadow-sm border-t-4 border-primary">
    <h3 class="text-2xl font-bold mb-6 text-primary flex items-center border-b pb-4">
        <!-- icon SVG --> Section Title
    </h3>
    <!-- Content: prose, charts, tables, sub-cards, etc. -->
</section>
```

Each section should use `scroll-margin-top` to prevent the sticky header from 
overlapping the section title:
```css
.content-section { scroll-margin-top: 5rem; }
```

### 5. Charts (Chart.js)

Place charts inside fixed-height containers:

```html
<div class="relative h-72">
    <canvas id="myChart"></canvas>
</div>
```

Initialize in JavaScript with theme colors:

```javascript
document.addEventListener('DOMContentLoaded', function() {
    const ctx = document.getElementById('myChart');
    if (ctx) {
        new Chart(ctx, {
            type: 'bar', // or 'doughnut', 'line', 'radar', etc.
            data: { /* ... */ },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { position: 'bottom' }
                }
            }
        });
    }
});
```

## Required JavaScript

### Scroll-Spy for Active Navigation

```javascript
document.addEventListener('DOMContentLoaded', function() {
    const sections = document.querySelectorAll('.content-section');
    const navLinks = document.querySelectorAll('.sidebar-link');
    const mainContent = document.querySelector('main');
    
    if (mainContent && sections.length && navLinks.length) {
        mainContent.addEventListener('scroll', () => {
            let current = '';
            sections.forEach(section => {
                const sectionTop = section.offsetTop - mainContent.offsetTop;
                if (mainContent.scrollTop >= sectionTop - 150) {
                    current = section.getAttribute('id');
                }
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href') === '#' + current) {
                    link.classList.add('active');
                }
            });
        });
    }
});
```

### Mobile Menu Toggle

```javascript
const menuButton = document.getElementById('mobile-menu-button');
const sidebar = document.getElementById('sidebar');
if (menuButton && sidebar) {
    menuButton.addEventListener('click', () => {
        sidebar.classList.toggle('-translate-x-full');
    });
    // Close sidebar when a nav link is clicked on mobile
    document.querySelectorAll('.sidebar-link').forEach(link => {
        link.addEventListener('click', () => {
            if (window.innerWidth < 768) {
                sidebar.classList.add('-translate-x-full');
            }
        });
    });
}
```

## Content Organization Guidelines

When analyzing source content for dashboard sections, aim for **5-8 sections** maximum. 
Group related topics rather than creating one section per paragraph.

**Good section breakdown:**
- Executive Summary / Overview
- Key Data & Metrics
- Analysis Section 1 (core argument)
- Analysis Section 2 (supporting evidence)
- Implications / Impact
- Recommendations / Outlook

**Avoid:**
- More than 10 sidebar items (overwhelming)
- Fewer than 3 sections (not enough to justify a dashboard)
- Sections with only 1-2 sentences (merge with adjacent sections)
