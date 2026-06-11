# Publishing Workflow · pjfarsi.github.io

This repo holds two unlisted project showcases served from a GitHub Pages user site:
- **`/ToHR/`** — Temple of Harm Reduction field guide docs
- **`/weedsy/`** — Weedsy brand system & pitch materials

## Project Structure

```
pjfarsi.github.io/
├── ToHR/
│   ├── index.html                  (landing page, links to docs)
│   ├── brand-reference.html
│   ├── case-for-support.html
│
├── weedsy/
│   ├── index.html                  (landing page, links to docs)
│   ├── brand-reference.html
│   ├── pitch-deck.html
│   ├── pitch-scroll.html
│   └── assets/
│       ├── canna-image.jpg
│       └── weedsy-deck.jpg
│
├── robots.txt                       (blocks both /ToHR/ and /weedsy/ from search)
```

## How It Works

### 1. **Unlisted by Design**
- No homepage at the root (`pjfarsi.github.io/` returns 404)
- Each project folder has an index page (`/ToHR/`, `/weedsy/`) that's **not linked from anywhere**
- `robots.txt` disallows crawlers from `/ToHR/` and `/weedsy/`
- **Result**: Only people you share the exact link with can access docs
- Search engines cannot index them

### 2. **Per-Project Index Pages**
Each project folder has an `index.html` landing page that:
- Lists the project's documents with descriptions
- Links to each document (HTML file)
- Matches the project's visual brand

**URLs:**
- `pjfarsi.github.io/ToHR/` → ToHR index page
- `pjfarsi.github.io/weedsy/` → weedsy index page
- Share the folder URL to anyone who needs to browse the docs

### 3. **Asset Paths (Critical)**
If your HTML files reference images (e.g., background images, illustrations), use **relative paths** from the file's location:

```html
<!-- ✓ CORRECT: HTML files at pjfarsi.github.io/PROJECTNAME/*.html →→ -->
<div style="background-image: url('assets/image.jpg');">

<!-- ✗ WRONG: This would break (points to domain root /assets/) →→ -->
<div style="background-image: url('../assets/image.jpg');">
```

**Why:** When you publish `weedsy/brand-reference.html`, the `../assets/` path (one level up) would resolve to the domain root, not the project's `weedsy/assets/` folder.

**If you need to add new images:**
1. Place them in `PROJECTNAME/assets/`
2. Reference them in HTML as: `url('assets/imagename.jpg')`
3. Use `Ctrl+S` to save locally, then sync to the repo

### 4. **Publishing Workflow**

#### To update an existing document:
```bash
# 1. Edit the HTML in your source folder (e.g., C:\CodeStack\weedsy\docs\)
# 2. Copy the updated .html file to the published folder:
cp ~/weedsy-source/pitch-deck.html ~/pjfarsi.github.io/weedsy/pitch-deck.html

# 3. Fix any asset paths if needed (../assets/ → assets/)
# 4. If it's a new document, update the project's index.html to link to it
# 5. Commit and push:
git add -A
git commit -m "Update weedsy: pitch-deck (revised)"
git push origin main
```

#### To add a new document:
```bash
# 1. Create the HTML (e.g., new-file.html)
# 2. Ensure all images use relative paths: url('assets/...')
# 3. Copy to the project folder
# 4. Update PROJECTNAME/index.html to add a new card linking to it
# 5. Commit, push, and verify at https://pjfarsi.github.io/PROJECTNAME/
```

### 5. **Index Pages (How to Update)**

Each `index.html` contains cards that link to documents. To add a new document to the index:

```html
<a class="card" href="new-file.html">
  <div class="row">
    <h2>Document Title</h2>
    <span class="arrow" aria-hidden="true">&rarr;</span>
  </div>
  <p>One-line description of the document.</p>
</a>
```

Insert this before the closing `</div>` of the `.cards` container.

## Verification

After you push, GitHub Pages deploys automatically (takes ~1–2 min). Verify by checking:
```
https://pjfarsi.github.io/PROJECTNAME/filename.html
```

**Status should be 200 OK** (not 404).

## FAQ

**Q: Why is the domain root (pjfarsi.github.io/) a 404?**
- By design. No homepage means no risk of accidental discovery. Share the folder link instead.

**Q: Can I add a homepage at the root?**
- Yes, if you add `pjfarsi.github.io/index.html`. It would link to `/ToHR/` and `/weedsy/` hubs.

**Q: Why do I get 404 when I try to browse the assets folder?**
- GitHub Pages doesn't serve directory listings. Assets must be referenced by exact filename in HTML (`url('assets/image.jpg')`).

**Q: What if I update an HTML file in the source but forget to copy it?**
- The published version won't update. Always copy from source to `pjfarsi.github.io/PROJECTNAME/` after editing.

**Q: Can I delete old documents?**
- Yes. Remove the `.html` file and the card from `index.html`, then push.

## Tech Stack

- **Hosting:** GitHub Pages (free, automatic HTTPS)
- **Framework:** Plain HTML + CSS (no dependencies, loads instantly)
- **Storage:** Git repository at github.com/pjfarsi/pjfarsi.github.io
- **Fonts:** Google Fonts CDN (loaded on page view, cached by browser)

## Contact

Questions about the publishing workflow? Add them to this guide or reach out to the maintainer.
