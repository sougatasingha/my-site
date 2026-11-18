# My Weekly Site

A Jekyll website that GitHub Pages builds and hosts for free. It has a home page and five other pages (Weekly, Projects, Resources, About, Contact), a light and dark theme, and an RSS feed. To post each week, you add one Markdown file.

---

## 1. Folder structure

```
my-site/
├── _config.yml              ← Site name, your name, links, URL settings (edit first)
├── index.html               ← HOME page
├── weekly.html              ← WEEKLY page: lists every post, with tag filters
├── projects.html            ← PROJECTS page (content comes from _data/projects.yml)
├── resources.html           ← RESOURCES page (content comes from _data/resources.yml)
├── about.md                 ← ABOUT page (plain Markdown, easy to edit)
├── contact.html             ← CONTACT page (email, socials, optional form)
├── 404.html                 ← "Page not found" page
│
├── _posts/                  ← ★ YOUR WEEKLY CONTENT GOES HERE ★
│   ├── 2026-11-09-week-01-welcome.md
│   └── 2026-11-16-week-02-sample-post.md
├── _drafts/
│   └── weekly-template.md   ← Copy this each week (drafts are never published)
│
├── _data/
│   ├── navigation.yml       ← Top menu items
│   ├── projects.yml         ← Project cards
│   └── resources.yml        ← Resource links
│
├── _layouts/                ← Page templates (default, page, post)
├── _includes/               ← Reusable pieces (head, header, footer, post card)
├── assets/
│   ├── css/style.css        ← All styling. Colors are at the top.
│   ├── js/main.js           ← Mobile menu, dark mode, tag filter
│   └── images/              ← Put post images here
│
├── Gemfile                  ← Only for previewing on your own computer
└── .gitignore
```

---

## 2. Make it live on GitHub Pages (about 10 minutes, one time)

### Step 1: Edit `_config.yml`
Change `title`, `tagline`, `author`, and `social`. Then set the URL settings:

| Your repo name          | `url`                         | `baseurl`     | Site address                          |
|-------------------------|-------------------------------|---------------|---------------------------------------|
| `USERNAME.github.io`    | `https://USERNAME.github.io`  | `""`          | `https://USERNAME.github.io`          |
| anything else, e.g. `my-site` | `https://USERNAME.github.io` | `"/my-site"` | `https://USERNAME.github.io/my-site` |

Using `USERNAME.github.io` as the repo name gives you the cleanest address.

### Step 2: Create the repository
1. Go to https://github.com/new
2. Repository name: `USERNAME.github.io` (replace USERNAME with your GitHub username), or any name you like
3. Set it to **Public**. GitHub Pages is free for public repos.
4. Click **Create repository**

### Step 3: Upload the files

**Option A: Browser, no tools needed**
1. In the new repo, click **"uploading an existing file"**
2. Drag in **everything inside** the `my-site` folder, not the folder itself. Folders are kept.
   - Your file manager may hide `.gitignore` because its name starts with a dot. That's fine; it's optional.
3. Click **Commit changes**

**Option B: Git command line**
```bash
cd my-site
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/USERNAME/USERNAME.github.io.git
git push -u origin main
```

### Step 4: Turn on Pages
1. In the repo, go to **Settings → Pages**
2. Under **Build and deployment → Source**, choose **Deploy from a branch**
3. Branch: **main**, folder: **/ (root)**, then click **Save**
4. Wait 1–2 minutes. Open the **Actions** tab to watch the build. A green check means it's live.
5. Your site is at the address shown at the top of **Settings → Pages**.

---

## 3. Weekly workflow: adding a new post

1. Copy `_drafts/weekly-template.md` into `_posts/`
2. Rename it to `YYYY-MM-DD-week-NN-short-title.md`, for example `2026-11-23-week-03-rag-evaluation.md`
3. Fill in the top section (front matter):
   ```yaml
   ---
   title: "Week 3: Evaluating RAG pipelines"
   week: 3
   tags: [RAG, Evaluation]
   summary: "What I learned measuring retrieval quality."
   ---
   ```
4. Write the post in Markdown below the second `---`
5. Commit it, either with **Add file → Upload files** on GitHub or with `git push`. The site rebuilds in about a minute.

The new post then shows up automatically on the Home page (as Latest), on the Weekly page (with its tag filter button), in the RSS feed, and in the previous/next links.

**Rules to remember**
- The date in the filename must be **today or earlier**. Future-dated posts stay hidden until that date.
- Images go in `assets/images/`. Use one like this: `![Description]({{ '/assets/images/my-chart.png' | relative_url }})`
- To hide a post without deleting it, add `published: false` to its front matter.
- Delete the two sample posts once you have real ones.

---

## 4. Customizing later

| I want to…                          | Edit this                                      |
|------------------------------------|------------------------------------------------|
| Rename, add or remove menu pages   | `_data/navigation.yml` and the matching page file |
| Change colors or fonts             | Top of `assets/css/style.css` (`:root` and `[data-theme="dark"]`) |
| Update projects                    | `_data/projects.yml`                           |
| Update resources                   | `_data/resources.yml`                          |
| Edit About text                    | `about.md`                                     |
| Add a contact form                 | Create a free form on formspree.io, then put its ID in `formspree_id` in `_config.yml` |
| Change the home page layout        | `index.html`                                   |

**Adding a new page** (for example `talks`): create `talks.md` with
```yaml
---
title: Talks
permalink: /talks/
---
```
then add it to `_data/navigation.yml`.

---

## 5. Custom domain (optional)
1. Buy a domain from any registrar.
2. At the registrar, add DNS records:
   - For a root domain (`example.com`), add four `A` records pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153` and `185.199.111.153`
   - For `www`, add a `CNAME` record pointing to `USERNAME.github.io`
3. In the repo, go to **Settings → Pages → Custom domain**, enter your domain, click Save, and tick **Enforce HTTPS** once it's available.
4. In `_config.yml`, set `url: "https://example.com"` and `baseurl: ""`.

---

## 6. Preview on your own computer (optional)
You need Ruby installed (https://www.ruby-lang.org). Then:
```bash
bundle install
bundle exec jekyll serve --drafts
```
Open http://localhost:4000. The `--drafts` flag also shows posts in `_drafts/`.

---

## Troubleshooting
- **Page is unstyled, or links are broken:** `baseurl` doesn't match the repo name. See Step 1.
- **404 right after enabling Pages:** wait 2 minutes and check the Actions tab.
- **New post not showing:** check that the filename date isn't in the future, and that the filename follows `YYYY-MM-DD-title.md`.
- **Build failed (red X in Actions):** open the failed run to see the error. It's usually a typo in the `---` front matter, such as a missing quote.
