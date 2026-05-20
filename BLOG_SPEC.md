# Blog Rebuild Spec — Vassily Lombard Science Blog

> **Audience for this file:** GitHub Copilot (or any AI coding assistant).  
> Read this entirely before touching any file. Follow every instruction in order.

---

## 1. Project Overview

**Goal:** A clean, modern personal blog hosted on GitHub Pages, built with Hugo + the PaperMod theme.  
The blog has two purposes:
1. A **Science Blog** — articles on scientific topics the author is passionate about.
2. An **About Me** page — a short personal introduction.

**Current problems to fix:**
- The site name is wrong (currently "Vassily Lombard Blog" — see target name below).
- The homepage is nearly empty and shows a broken/ugly layout (giant blue triangle SVG artefact from PaperMod's default logo).
- No posts or About page exist yet.
- The GitHub Actions workflow (`hugo.yml`) was deleted; deployment is done by committing the `public/` folder to `docs/` and enabling GitHub Pages on that branch/folder.

---

## 2. Target Site Name & URL

| Field | Value |
|---|---|
| Site title | **Vassily Lombard — Science & Curiosity** |
| Base URL | Update `hugo.toml` `baseURL` to match the actual GitHub Pages URL: `https://<username>.github.io/<repo-name>/` |
| Author | Vassily Lombard |

---

## 3. Repository Structure (current → target)

```
repo/
├── .github/workflows/        # leave empty for now (no CI)
├── archetypes/
│   └── default.md            # keep as-is
├── content/
│   ├── posts/                # blog articles go here
│   │   └── _index.md         # CREATE: section index
│   └── about.md              # CREATE: About Me page
├── docs/                     # Hugo outputs here (GitHub Pages source)
├── themes/
│   └── PaperMod/             # git submodule — do not edit files inside
├── static/
│   └── favicon.ico           # OPTIONAL: add a favicon later
├── .gitmodules               # keep as-is
├── .hugo_build.lock          # keep as-is
└── hugo.toml                 # EDIT: full replacement (see Section 4)
```

---

## 4. `hugo.toml` — Full Replacement

Replace the entire contents of `hugo.toml` with the following:

```toml
baseURL = "https://<USERNAME>.github.io/<REPO>/"   # ← replace with real values
languageCode = "en-us"
title = "Vassily Lombard — Science & Curiosity"
theme = "PaperMod"
paginate = 8

[params]
  author = "Vassily Lombard"
  description = "A blog about science, curiosity, and the ideas that matter."
  defaultTheme = "auto"          # auto = follows OS light/dark preference
  ShowReadingTime = true
  ShowShareButtons = false
  ShowPostNavLinks = true
  ShowBreadCrumbs = true
  ShowCodeCopyButtons = true
  ShowToc = true
  TocOpen = false
  disableScrollToTop = false
  comments = false

  [params.homeInfoParams]
    Title = "Hello, I'm Vassily 👋"
    Content = "I write about science, physics, biology, and the ideas that keep me up at night. Welcome to my corner of the internet."

  [[params.socialIcons]]
    name = "github"
    url = "https://github.com/<USERNAME>"

[menu]
  [[menu.main]]
    identifier = "posts"
    name = "Posts"
    url = "/posts/"
    weight = 10

  [[menu.main]]
    identifier = "about"
    name = "About"
    url = "/about/"
    weight = 20

  [[menu.main]]
    identifier = "search"
    name = "Search"
    url = "/search/"
    weight = 30

[outputs]
  home = ["HTML", "RSS", "JSON"]   # JSON needed for search

[markup]
  [markup.highlight]
    style = "monokai"
    lineNos = false
```

> **Note to Copilot:** Replace `<USERNAME>` and `<REPO>` with the actual GitHub username and repository name before saving.

---

## 5. Files to Create

### 5a. `content/posts/_index.md`

```markdown
---
title: "Posts"
description: "All articles on science and curiosity."
---
```

### 5b. `content/about.md`

```markdown
---
title: "About Me"
date: 2026-01-01
layout: "page"
url: "/about/"
summary: "A bit about who I am."
---

Hi, I'm Vassily — a curious person fascinated by science in all its forms.

<!-- Replace the paragraph below with your own words -->

I'm particularly drawn to [your interests, e.g. physics, neuroscience, ecology].
This blog is where I share what I'm learning, thinking about, and excited by.

Feel free to reach out via GitHub.
```

### 5c. `content/search.md`

PaperMod has a built-in search feature. Create this file to enable it:

```markdown
---
title: "Search"
layout: "search"
url: "/search/"
summary: "Search all posts"
placeholder: "Search articles..."
---
```

### 5d. First sample post — `content/posts/welcome.md`

```markdown
---
title: "Welcome to My Science Blog"
date: 2026-05-20
description: "Why I started writing about science and what to expect."
tags: ["meta", "introduction"]
draft: false
---

This is the first post. Replace this with a real introduction.

Science is a way of thinking, not just a collection of facts. I started this blog
to force myself to write clearly about ideas I find fascinating — because writing
is thinking.

Expect posts on physics, biology, mathematics, and anything else that catches my eye.
```

---

## 6. Build & Deploy Steps

After making all file changes above, run these commands locally:

```bash
# 1. Remove old generated output
rm -rf docs/*

# 2. Build the site, outputting to /docs (GitHub Pages source)
hugo --destination docs --minify

# 3. Commit and push everything
git add .
git commit -m "Rebuild site: new config, about page, first post"
git push origin main
```

Then in GitHub → Settings → Pages:
- **Source:** Deploy from branch `main`, folder `/docs`

The site will be live at `https://<USERNAME>.github.io/<REPO>/` within a minute.

---

## 7. How to Add Content in the Future

### Add a new blog post

Create a file at `content/posts/my-post-title.md`:

```markdown
---
title: "My Post Title"
date: 2026-06-01
description: "One-sentence summary shown in listings."
tags: ["physics", "relativity"]   # optional, for filtering
draft: false
---

Your content here in standard Markdown.
```

Then rebuild and push (repeat Step 6).

### Add a new standalone page

Create `content/my-page.md` with a front-matter `url: "/my-page/"`, write your content, then add it to the `[menu]` section in `hugo.toml` if you want it in the nav.

### Change the homepage intro text

Edit the `[params.homeInfoParams]` block in `hugo.toml`.

### Change the theme colours (PaperMod custom CSS)

Create `assets/css/extended/custom.css` and override CSS variables there. PaperMod will automatically pick it up. Example:

```css
:root {
  --primary: #1a1a2e;
  --secondary: #16213e;
  --accent: #e94560;
}
```

---

## 8. What NOT to Change

- Do **not** edit any files inside `themes/PaperMod/` — it is a git submodule. Override via `layouts/` or `assets/` in the root instead.
- Do **not** delete `docs/` from `.gitignore` (if present) — GitHub Pages needs it committed.
- Do **not** re-add a GitHub Actions workflow unless you want to automate builds; the manual `hugo --destination docs` approach is simpler for a solo blog.

---

## 9. Checklist for Copilot

- [ ] Replace `hugo.toml` entirely with the config in Section 4 (fill in `<USERNAME>` and `<REPO>`)
- [ ] Create `content/posts/_index.md`
- [ ] Create `content/about.md`
- [ ] Create `content/search.md`
- [ ] Create `content/posts/welcome.md`
- [ ] Run `hugo --destination docs --minify`
- [ ] Commit and push all changes
