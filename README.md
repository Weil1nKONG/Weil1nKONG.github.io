# Post Dataset Manager

A self-contained HTML tool for creating and publishing posts to GitHub Pages. Built for GEO (Generative Engine Optimization) research — each post becomes a real webpage with a customizable publish time.

**Live tool:** [weil1nkong.github.io/post-dataset-tool.html](https://weil1nkong.github.io/post-dataset-tool.html)

---

## Features

- Write posts with title, author, content, group category, and a **customizable publish time** (core feature)
- One-click **publish to GitHub Pages** via GitHub API
- Each post becomes a standalone HTML page at `posts/{slug}.html`
- **Group posts by category** — filter in the manager, index page organizes by group
- Auto-generated post index at `/posts/` — grouped by category
- Edit, update, unpublish, or delete posts
- Local draft mode with localStorage persistence
- Export/import dataset as HTML with embedded JSON
- No server required — single HTML file, runs entirely in the browser

---

## Quick Start

### 1. Open the tool

```
https://weil1nkong.github.io/post-dataset-tool.html
```

### 2. Configure GitHub Token (first time only)

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Generate a **Classic token** with `repo` scope
3. In the tool, click **Settings** (top-right) → paste the token → **Test Connection** → **Save**

### 3. Create & Publish

1. Fill in Title, Author, Group (e.g. Tech, Research, Cooking), Content
2. Set the Publish Time (can be any past or future date)
3. Click **Save Locally** (saves as draft)
4. Click **Publish to GitHub** (live on the internet)

---

## Interface

```
+-------------------------------+---------------------------+
|  Post Dataset Manager         |  3 posts (2 published)    |
+-------------------------------+---------------------------+
|  [Search...] [Sort][Group v]  |  New Post / Edit Post      |
|                               |                            |
|  +-- Post Card (Draft) --+    |  Title: [............]     |
|  | Title           Time  |    |  Slug:  [............]     |
|  | [Draft][Tech] Author  |    |  Author:[............]     |
|  | Preview text...       |    |  Group: [............]     |
|  +-----------------------+    |  Content:                 |
|                               |  [..................]     |
|  +-- Post Card (Published)-+  |  Publish Time: [picker]    |
|  | Title           Time   |   |  [Update]                  |
|  | [Published][Research]  |   |                            |
|  | Preview text...        |   |  [Save Locally] [New]      |
|  +------------------------+   |  [Publish to GitHub]       |
|                               |  [Unpublish] [Delete]      |
+-------------------------------+---------------------------+
|  Tip text   [Export] [Import] [Clear All]                   |
+------------------------------------------------------------+
```

---

## Workflow

### Publishing a new post
```
Write → Save Locally → Publish to GitHub → Live at /posts/{slug}.html
```

### Updating a published post
```
Click card → Edit → Save Locally → Update on GitHub → Live updated
```

### Unpublishing
```
Click card → Unpublish → Removed from web, kept locally as draft
```

### Deleting
```
Click card → Delete Post → Removed from both local storage and GitHub
```

---

## Data Structure

Each post is stored as JSON:

```json
{
  "id":            "post_1718323200000_abc123",
  "title":         "Best Laptops for Students",
  "slug":          "best-laptops-for-students",
  "author":        "TechReview",
  "group":         "Tech",
  "content":       "After testing 20 laptops...",
  "publishTime":   "2025-01-01T09:00",
  "createdAt":     "2026-06-14T15:30",
  "updatedAt":     "2026-06-14T15:35",
  "published":     true,
  "publishedUrl":  "https://weil1nkong.github.io/posts/best-laptops-for-students.html",
  "publishedSha":  "abc123def456..."
}
```

Exported HTML files contain the full JSON inside a `<script type="application/json" id="dataset-json">` tag.

---

## Export & Import

| Action | Button | Output |
|--------|--------|--------|
| Export | `Export Dataset (HTML)` | Downloads a self-contained HTML file with all posts |
| Import | `Import Dataset` | Loads posts from a previously exported file |

Exports include semantic `<article>` tags and `<time datetime="...">` markup.

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Ctrl+S` / `Cmd+S` | Save post locally |
| `Esc` | Cancel editing / Close modal |

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Publish fails | Check Settings → Token is configured and has `repo` scope |
| Test Connection fails | Re-paste token; make sure it's a **Classic** token, not Fine-grained |
| Published page is 404 | Wait a few seconds for Pages deployment; check slug spelling |
| Data lost after refresh | Data is in localStorage — don't use private mode; export regularly |

---

## File Structure

```
dataset/
  post-dataset-tool.html   ← The tool itself (open in browser)
  README.md                ← This guide
  网页.txt                  ← Usage guide (Chinese)
```

---

## Notes

- Data is stored in your browser's `localStorage` — different browsers/devices have separate data
- The GitHub token is also stored in localStorage — never commit it to git
- Published posts live at `https://weil1nkong.github.io/posts/{slug}.html`
- The post index is at `https://weil1nkong.github.io/posts/` — organized by group
- Group is a free-text field; preset suggestions include Tech, Research, Cooking, Life, News, Other
- Filter posts by group using the dropdown in the search bar
