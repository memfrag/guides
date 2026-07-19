# Guides

Coding guides and architecture documents, published as static HTML pages via GitHub Pages.

**Live site:** https://memfrag.github.io/guides/

## Structure

```
index.html         Landing page, lists all guides (reads guides.json)
guides.json         Manifest of guides shown on the index page
assets/style.css    Shared stylesheet used by all pages
docs/               Individual guide pages
```

## Adding a new guide

1. Create `docs/your-guide.html`. Use `docs/example-guide.html` as a starting template
   (it links to `../assets/style.css` and back to the index).
2. Add an entry to `guides.json`:
   ```json
   {
     "title": "Your Guide",
     "path": "docs/your-guide.html",
     "description": "One-line summary.",
     "tags": ["optional", "tags"],
     "updated": "YYYY-MM-DD"
   }
   ```
3. Commit and push. The index page picks up new entries automatically.

## Local preview

```
python3 -m http.server 8000
```

Then open http://localhost:8000/.
