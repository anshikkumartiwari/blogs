# Blogs Blueprint & Setup Guide

This document contains everything needed to spin up your standalone blog system in [github.com/anshikkumartiwari/blogs](https://github.com/anshikkumartiwari/blogs.git).

---

## 1. Recommended Repository File Tree

```text
blogs/
├── index.html            <-- Main blog listing page with search & featured article
├── article.html          <-- Dynamic Markdown reader (loads via ?a=filename.md)
├── style.css             <-- Styling tokens, layout, typography & theme support
├── manifest.json         <-- Article registry with metadata
├── template.md           <-- Starter blueprint article
├── article1.md           <-- Sample article 1
├── article2.md           <-- Sample article 2
└── article3.md           <-- Sample article 3
```

---

## 2. Source Code Files

### `manifest.json`
```json
[
  {
    "file": "article1.md",
    "title": "My experience with interview at flipkart",
    "subtitle": "A personal review of the software engineering interview process and technical rounds",
    "date": "Apr 7, 2026",
    "readTime": "11 min read",
    "description": "A walkthrough of my interview experience at Flipkart. I discuss the technical problem-solving rounds, system design questions, and the key preparation strategies that helped me navigate the process."
  },
  {
    "file": "article2.md",
    "title": "Designing Quiet Software in a Loud World",
    "subtitle": "An essay on building focused, minimalist, and deeply respectful digital environments",
    "date": "Mar 12, 2026",
    "readTime": "4 min read",
    "description": "In an industry obsessed with user retention, notifications, and continuous engagement, how do we design software that is silent, respectful, and fully in service of the user?"
  },
  {
    "file": "article3.md",
    "title": "WebV: Wrapping Web Pages in C & GTK",
    "subtitle": "Building a lightweight, Linux-native browser wrapper with GTK3 and WebKit2",
    "date": "Feb 28, 2026",
    "readTime": "7 min read",
    "description": "How to engineer a fast, native browser launcher in C using the GTK3 framework to wrap web interfaces into beautiful GUI windows without the memory overhead of Chromium or Electron."
  }
]
```

---

### `style.css`
```css
/* ==========================================================================
   DESIGN TOKENS & TYPOGRAPHY
   ========================================================================== */
@import url('https://api.fontshare.com/v2/css?f=satoshi@300,400,500,700,900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');

:root {
  --bg:         #FAF8F5;
  --surface:    #F3ECE2;
  --surface-hv: #EBE3D7;
  --fg:         #1E1E1E;
  --muted:      #6B655F;
  --accent:     #B37D56;
  --accent-bg:  rgba(179,125,86,.09);
  --border:     #E6DDD2;
  --border-hv:  #D1C5B6;

  --f-head: 'Satoshi','Inter',sans-serif;
  --f-body: 'Inter',sans-serif;
  --f-mono: 'JetBrains Mono',monospace;

  --nav-h: 64px;
  --wrap:  860px;

  --t-fast:   150ms ease;
  --t-normal: 280ms ease;
}

html[data-theme="dark"] {
  --bg:         #111110;
  --surface:    #1B1B19;
  --surface-hv: #262623;
  --fg:         #EBEAE6;
  --muted:      #9E9890;
  --accent:     #E0A070;
  --accent-bg:  rgba(224,160,112,.09);
  --border:     #2C2B29;
  --border-hv:  #3E3C39;
}

@media (prefers-color-scheme: dark) {
  html:not([data-theme="light"]) {
    --bg:         #111110;
    --surface:    #1B1B19;
    --surface-hv: #262623;
    --fg:         #EBEAE6;
    --muted:      #9E9890;
    --accent:     #E0A070;
    --accent-bg:  rgba(224,160,112,.09);
    --border:     #2C2B29;
    --border-hv:  #3E3C39;
  }
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
* { -webkit-font-smoothing: antialiased; }
a { color: inherit; text-decoration: none; }
body {
  background: var(--bg);
  color: var(--fg);
  font-family: var(--f-body);
  line-height: 1.7;
  transition: background var(--t-normal), color var(--t-normal);
}

.wrap {
  max-width: var(--wrap);
  margin: 0 auto;
  padding: 0 2rem;
}

/* NAVBAR */
.nav {
  position: sticky;
  top: 0;
  height: var(--nav-h);
  background: rgba(250,248,245,.92);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  z-index: 100;
  display: flex;
  align-items: center;
}
html[data-theme="dark"] .nav {
  background: rgba(17,17,16,.92);
}
.nav-inner {
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.nav-brand {
  font-family: var(--f-head);
  font-weight: 700;
  font-size: 1.15rem;
  letter-spacing: -0.02em;
}
.nav-right {
  display: flex;
  align-items: center;
  gap: 1.25rem;
  font-size: 0.9rem;
}
.nav-link {
  color: var(--muted);
  transition: color var(--t-fast);
}
.nav-link:hover {
  color: var(--accent);
}

/* FOOTER */
.site-footer {
  border-top: 1px solid var(--border);
  padding: 2.5rem 0;
  font-size: 0.82rem;
  color: var(--muted);
  text-align: center;
  margin-top: 5rem;
}

/* ==========================================================================
   BLOG LISTING STYLES
   ========================================================================== */
.blogs-hero {
  padding: 6rem 0 3rem;
}
.blogs-meta-label {
  font-family: var(--f-mono);
  font-size: 0.72rem;
  text-transform: uppercase;
  color: var(--accent);
  letter-spacing: 0.12em;
  margin-bottom: 0.75rem;
  display: block;
}
.blogs-title {
  font-family: var(--f-head);
  font-size: clamp(2.6rem, 6vw, 4rem);
  font-weight: 700;
  letter-spacing: -0.04em;
  line-height: 1.05;
  margin-bottom: 0.8rem;
}
.blogs-subtitle {
  color: var(--muted);
  font-size: clamp(1.05rem, 2vw, 1.25rem);
  max-width: 620px;
  margin-bottom: 3rem;
}
.search-container {
  position: relative;
  border-bottom: 1px solid var(--border);
  margin-bottom: 1.5rem;
}
.search-input {
  width: 100%;
  background: transparent;
  border: none;
  color: var(--fg);
  font-family: var(--f-head);
  font-size: clamp(1.2rem, 3vw, 1.6rem);
  padding: 0.6rem 0.5rem 0.6rem 2.2rem;
  outline: none;
}
.search-input::placeholder { color: var(--border-hv); opacity: 0.85; }
.search-icon-svg {
  position: absolute;
  left: 0.2rem;
  top: 50%;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  fill: none;
  stroke: var(--border-hv);
  stroke-width: 2;
  pointer-events: none;
}
.search-input:focus + .search-icon-svg { stroke: var(--accent); }
.search-count {
  font-family: var(--f-mono);
  font-size: 0.72rem;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  display: block;
}

.featured-card {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 3.5rem;
  align-items: center;
  padding: 2.5rem 0;
  border-bottom: 1px solid var(--border);
  transition: border-color var(--t-normal);
}
.featured-card:hover { border-color: var(--accent); }
.featured-badge {
  font-family: var(--f-mono);
  font-size: 0.68rem;
  background: var(--accent-bg);
  color: var(--accent);
  padding: 0.2rem 0.55rem;
  border-radius: 4px;
  display: inline-block;
  margin-bottom: 1rem;
}
.featured-title {
  font-family: var(--f-head);
  font-size: clamp(1.6rem, 4vw, 2.4rem);
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 0.8rem;
  transition: color var(--t-fast);
}
.featured-card:hover .featured-title { color: var(--accent); }
.featured-desc { color: var(--muted); font-size: 1rem; margin-bottom: 1.2rem; }
.featured-thumb-wrap {
  aspect-ratio: 16/10;
  border-radius: 6px;
  border: 1px solid var(--border);
  background: var(--surface);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}
.featured-monogram {
  font-family: var(--f-head);
  font-weight: 700;
  font-size: clamp(3.5rem, 8vw, 5rem);
  color: var(--accent);
}
.meta-row {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.78rem;
  color: var(--muted);
}
.meta-sep { color: var(--border); }

.articles-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem 2.5rem;
  padding: 3rem 0 6rem;
}
.editorial-grid-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border-bottom: 1px solid var(--border);
  padding-bottom: 2rem;
  transition: transform var(--t-normal), border-color var(--t-normal);
}
.editorial-grid-card:hover {
  transform: translateY(-2px);
  border-color: var(--accent);
}
.grid-card-thumb-wrap {
  aspect-ratio: 16/9;
  border-radius: 4px;
  border: 1px solid var(--border);
  background: var(--surface);
  margin-bottom: 1.2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
.grid-card-title {
  font-family: var(--f-head);
  font-size: 1.25rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}
.editorial-grid-card:hover .grid-card-title { color: var(--accent); }
.grid-card-desc {
  font-size: 0.9rem;
  color: var(--muted);
  line-height: 1.55;
  margin-bottom: 1.25rem;
  flex-grow: 1;
}

/* ==========================================================================
   ARTICLE READER STYLES
   ========================================================================== */
.article-container {
  max-width: 760px;
  margin: 0 auto;
  padding: 4rem 1.5rem 7rem;
}
.article-back-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-family: var(--f-mono);
  font-size: 0.85rem;
  color: var(--muted);
  margin-bottom: 2.5rem;
  transition: color var(--t-fast), transform var(--t-fast);
}
.article-back-btn:hover {
  color: var(--accent);
  transform: translateX(-3px);
}
.article-header {
  border-bottom: 1px solid var(--border);
  padding-bottom: 2.5rem;
  margin-bottom: 3rem;
}
.article-page-title {
  font-family: var(--f-head);
  font-size: clamp(2rem, 5vw, 3.2rem);
  font-weight: 700;
  line-height: 1.15;
  margin-bottom: 1rem;
}
.article-page-subtitle {
  font-size: clamp(1.1rem, 2.2vw, 1.35rem);
  color: var(--muted);
  line-height: 1.45;
  margin-bottom: 1.75rem;
}
.article-body h1, .article-body h2, .article-body h3 {
  font-family: var(--f-head);
  font-weight: 700;
  margin-top: 2.75rem;
  margin-bottom: 1rem;
}
.article-body h2 {
  font-size: 1.6rem;
  border-bottom: 1px solid var(--border);
  padding-bottom: 0.4rem;
}
.article-body p { margin-bottom: 1.7rem; }
.article-body blockquote {
  border-left: 3px solid var(--accent);
  padding: 0.4rem 0 0.4rem 1.4rem;
  margin: 2rem 0;
  font-style: italic;
  color: var(--muted);
}
.article-body pre {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 1.2rem;
  margin: 2rem 0;
  overflow-x: auto;
}
.article-body code {
  font-family: var(--f-mono);
  font-size: 0.85em;
  background: var(--surface);
  padding: 0.2rem 0.4rem;
  border-radius: 4px;
}
.article-body pre code { background: none; padding: 0; }
.article-body table {
  width: 100%;
  border-collapse: collapse;
  margin: 2rem 0;
}
.article-body th, .article-body td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--border);
  text-align: left;
}

@media (max-width: 800px) {
  .featured-card { grid-template-columns: 1fr; gap: 2rem; }
  .articles-grid { grid-template-columns: 1fr; }
}
```

---

### `index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blogs &amp; Essays — Anshik Kumar Tiwari</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAVBAR -->
  <nav class="nav">
    <div class="nav-inner">
      <a href="index.html" class="nav-brand">Anshik's Blogs</a>
      <div class="nav-right">
        <a href="https://anshikkumartiwari.github.io" class="nav-link">← Portfolio</a>
      </div>
    </div>
  </nav>

  <!-- HERO & SEARCH SECTION -->
  <header class="blogs-hero">
    <div class="wrap">
      <span class="blogs-meta-label">Selected Writings</span>
      <h1 class="blogs-title">Blogs &amp; Essays</h1>
      <p class="blogs-subtitle">An archive of deep-dives, essays, and technical notes on systems architecture, languages, and mathematical modeling.</p>
      
      <div class="search-container">
        <input type="text" id="search-bar" class="search-input" placeholder="Search writings by title or topic..." aria-label="Search writings">
        <svg class="search-icon-svg" viewBox="0 0 24 24">
          <circle cx="11" cy="11" r="8"></circle>
          <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
        </svg>
      </div>
      <span class="search-count" id="results-count">Scanning articles...</span>
    </div>
  </header>

  <!-- ARTICLES LISTING -->
  <main class="wrap">
    <div class="featured-article-container" id="featured-section"></div>
    <div class="articles-grid" id="grid-section"></div>
  </main>

  <footer class="site-footer">
    <span>&copy; Anshik Kumar Tiwari</span>
  </footer>

  <script>
    let allArticles = [];
    let searchQuery = "";

    document.addEventListener("DOMContentLoaded", () => {
      loadWritings();
      setupSearch();
    });

    async function loadWritings() {
      try {
        const res = await fetch("manifest.json");
        if (res.ok) {
          allArticles = await res.json();
        }
      } catch (e) {
        console.warn("Could not load manifest.json", e);
      }

      if (allArticles.length === 0) {
        document.getElementById("featured-section").innerHTML = `
          <div style="text-align:center;color:var(--muted);padding:4rem;font-family:var(--f-mono);">No articles found in manifest.json.</div>
        `;
        return;
      }
      renderWritings();
    }

    function setupSearch() {
      const searchBar = document.getElementById("search-bar");
      searchBar.addEventListener("input", (e) => {
        searchQuery = e.target.value.toLowerCase().trim();
        renderWritings();
      });
    }

    function renderWritings() {
      const featuredContainer = document.getElementById("featured-section");
      const gridContainer = document.getElementById("grid-section");
      const countLabel = document.getElementById("results-count");

      const filtered = allArticles.filter(art => {
        return searchQuery === "" ||
          art.title.toLowerCase().includes(searchQuery) ||
          (art.description && art.description.toLowerCase().includes(searchQuery)) ||
          (art.subtitle && art.subtitle.toLowerCase().includes(searchQuery));
      });

      countLabel.textContent = searchQuery !== "" 
        ? `Found ${filtered.length} matching article${filtered.length === 1 ? '' : 's'}`
        : `Showing all ${filtered.length} articles`;

      if (filtered.length === 0) {
        featuredContainer.innerHTML = "";
        gridContainer.innerHTML = `<div style="grid-column: 1/-1; text-align:center; color:var(--muted); padding:4rem 0;">No articles match your query.</div>`;
        return;
      }

      const featured = filtered[0];
      const others = filtered.slice(1);

      featuredContainer.innerHTML = `
        <a href="article.html?a=${featured.file}" class="featured-card">
          <div>
            <span class="featured-badge">Featured Essay</span>
            <h2 class="featured-title">${featured.title}</h2>
            <p class="featured-desc">${featured.description || featured.subtitle || ""}</p>
            <div class="meta-row">
              <span>Anshik Kumar Tiwari</span>
              <span class="meta-sep">•</span>
              <span>${featured.date}</span>
              <span class="meta-sep">•</span>
              <span>${featured.readTime}</span>
            </div>
          </div>
          <div class="featured-thumb-wrap">
            <div class="featured-monogram">${featured.title.charAt(0)}</div>
          </div>
        </a>
      `;

      gridContainer.innerHTML = others.map(art => `
        <a href="article.html?a=${art.file}" class="editorial-grid-card">
          <div>
            <div class="grid-card-thumb-wrap">
              <div class="featured-monogram" style="font-size:3rem;">${art.title.charAt(0)}</div>
            </div>
            <h3 class="grid-card-title">${art.title}</h3>
            <p class="grid-card-desc">${art.description || art.subtitle || ""}</p>
          </div>
          <div class="meta-row" style="margin-top:1.5rem;">
            <span>${art.date}</span>
            <span class="meta-sep">•</span>
            <span>${art.readTime}</span>
          </div>
        </a>
      `).join('');
    }
  </script>
</body>
</html>
```

---

### `article.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Reading Article... — Anshik Kumar Tiwari</title>
  <link rel="stylesheet" href="style.css">
</head>
<body class="article-page">

  <nav class="nav">
    <div class="nav-inner">
      <a href="index.html" class="nav-brand">Anshik's Blogs</a>
      <div class="nav-right">
        <a href="index.html" class="nav-link">← All Writings</a>
      </div>
    </div>
  </nav>

  <div class="article-container">
    <a href="index.html" class="article-back-btn">
      ← Back to articles
    </a>

    <div id="loading" style="text-align: center; padding: 4rem 0; color: var(--muted); font-family: var(--f-mono);">
      Loading article...
    </div>

    <article id="article-content" style="display: none;">
      <header class="article-header">
        <h1 class="article-page-title" id="meta-title"></h1>
        <p class="article-page-subtitle" id="meta-subtitle"></p>
        <div class="meta-row" style="margin-top: 1rem;">
          <span id="meta-author">Anshik Kumar Tiwari</span>
          <span class="meta-sep">•</span>
          <span id="meta-date"></span>
          <span class="meta-sep">•</span>
          <span id="meta-readtime"></span>
        </div>
      </header>
      <div class="article-body" id="rendered-body"></div>
    </article>
  </div>

  <footer class="site-footer">
    <span>&copy; Anshik Kumar Tiwari</span>
  </footer>

  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <script>
    document.addEventListener("DOMContentLoaded", loadArticle);

    function parseFrontMatter(text) {
      const regex = /^---\r?\n([\s\S]*?)\r?\n---/;
      const match = text.match(regex);
      const metadata = {};
      let bodyContent = text;

      if (match) {
        bodyContent = text.replace(match[0], '').trim();
        const lines = match[1].split('\n');
        for (const line of lines) {
          const colonIdx = line.indexOf(':');
          if (colonIdx !== -1) {
            const key = line.slice(0, colonIdx).trim();
            let val = line.slice(colonIdx + 1).trim().replace(/^['"]|['"]$/g, '');
            metadata[key] = val;
          }
        }
      }
      return { metadata, bodyContent };
    }

    async function loadArticle() {
      const params = new URLSearchParams(window.location.search);
      let file = params.get("a") || "template.md";
      if (!file.endsWith(".md")) file += ".md";

      try {
        let manifestMeta = {};
        try {
          const mRes = await fetch("manifest.json");
          if (mRes.ok) {
            const list = await mRes.json();
            manifestMeta = list.find(item => item.file === file) || {};
          }
        } catch (_) {}

        const response = await fetch(file);
        if (!response.ok) throw new Error("Article file not found");

        const raw = await response.text();
        const { metadata: frontMeta, bodyContent } = parseFrontMatter(raw);
        const meta = { ...manifestMeta, ...frontMeta };

        document.getElementById("meta-title").textContent = meta.title || "Untitled";
        if (meta.subtitle) {
          document.getElementById("meta-subtitle").textContent = meta.subtitle;
        } else {
          document.getElementById("meta-subtitle").style.display = "none";
        }
        document.getElementById("meta-date").textContent = meta.date || "";
        document.getElementById("meta-readtime").textContent = meta.readTime || "";
        document.title = `${meta.title || "Article"} — Anshik Kumar Tiwari`;

        document.getElementById("rendered-body").innerHTML = marked.parse(bodyContent);
        document.getElementById("loading").style.display = "none";
        document.getElementById("article-content").style.display = "block";
      } catch (err) {
        document.getElementById("loading").innerHTML = `
          <div style="color:var(--accent);">Unable to load ${file}.</div>
          <p style="margin-top:1rem;"><a href="index.html">Return to all articles</a></p>
        `;
      }
    }
  </script>
</body>
</html>
```

---

### `template.md`
```markdown
---
title: "Article Title Blueprint"
subtitle: "A description of the template and format specification"
date: "May 24, 2026"
readTime: "5 min read"
description: "This is a blueprint/template showing all supported Markdown features for the blog engine."
---

# Heading 1

This is a standard paragraph with **bold text** and *italicized text*.

## Heading 2

> "Simplicity is the ultimate sophistication."

### Code Blocks

```js
function greet(user) {
  console.log(`Hello, ${user}!`);
}
```

### Tables

| Technology | Role |
| :--- | :--- |
| Marked.js | Markdown Parser |
| Vanilla CSS | Aesthetics & Design |
```

---

## 3. How to Initialize the New Repo

1. Clone or initialize the empty repository locally:
   ```bash
   git clone https://github.com/anshikkumartiwari/blogs.git
   cd blogs
   ```
2. Copy the contents of the files above into their respective paths (`index.html`, `article.html`, `style.css`, `manifest.json`, `template.md`).
3. Commit and push:
   ```bash
   git add .
   git commit -m "initial blog engine setup"
   git push origin main
   ```
4. Enable **GitHub Pages** under `Settings -> Pages -> Deploy from a branch (main)`.
   Your blog will immediately go live at `https://anshikkumartiwari.github.io/blogs/`.
