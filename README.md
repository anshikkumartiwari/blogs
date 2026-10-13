# Blogs Content Repository

This repository acts as the headless content store for [anshikkumartiwari.github.io](https://anshikkumartiwari.github.io).

## Directory Structure

Each blog article has its own folder containing `article.md`, a `meta.json` file, an optional thumbnail image (`thumb.*`), and any images or assets:

```text
blogs/
├── manifest.json            # Registry index for quick listing
├── README.md
├── blog1/
│   ├── meta.json            # Post metadata (title, subtitle, date, etc.)
│   ├── article.md           # Markdown content
│   ├── thumb.png            # Card thumbnail (png, jpg, webp, jpeg)
│   └── (local images...)
├── blog2/
│   ├── meta.json
│   ├── article.md
│   └── (assets...)
└── blog3/
    ├── meta.json
    ├── article.md
    └── (assets...)
```

---

## File Specifications

### 1. `meta.json`
Stores metadata for the article. The `title` and `subtitle` / `description` are shared between the blog cards and the full article page:

```json
{
  "title": "Article Title",
  "subtitle": "A short summary or sub-description of the article",
  "description": "A short summary or sub-description of the article",
  "date": "Apr 14, 2026",
  "readTime": "5 min read",
  "slug": "article-url-slug",
  "author": "Anshik Kumar Tiwari",
  "authorImage": "../images/profile.jpg"
}
```

### 2. `article.md`
Standard GitHub-Flavored Markdown file containing the article body.
Relative image links like `![diagram](diagram.png)` inside `article.md` are automatically resolved to this repository by the portfolio reader.

### 3. Thumbnails (`thumb.*`)
Place any image named:
- `thumb.png`
- `thumb.jpg` / `thumb.jpeg`
- `thumb.webp`

inside the blog folder. The portfolio engine will automatically detect and display it as the card's thumbnail. If no thumbnail is provided, it falls back to a clean typographic monogram.

---

## Adding a New Post

1. Create a new folder (e.g., `blog4/`).
2. Add your content in `blog4/article.md`.
3. Add `blog4/meta.json` with the required metadata.
4. *(Optional)* Add `blog4/thumb.png` (or `.jpg` / `.webp`).
5. Register the new post entry in the root `manifest.json`.
6. Commit and push:
   ```bash
   git add .
   git commit -m "add blog4"
   git push origin main
   ```
Your portfolio will immediately reflect the new article live!
