# Soteria - GitHub Pages

This folder contains the public-facing website for Soteria, hosted via GitHub Pages.

## Enabling GitHub Pages

To host this site on GitHub:

1. Push this repository to GitHub
2. Go to your repository on GitHub
3. Navigate to **Settings** → **Pages**
4. Under **Source**, select:
   - **Branch:** `main` (or your default branch)
   - **Folder:** `/gh-pages`
5. Click **Save**

Your site will be available at: `https://YOUR_USERNAME.github.io/soteria/`

## Alternative: Using /docs folder

If GitHub doesn't allow selecting `/gh-pages`, you can:

1. Rename this folder from `gh-pages` to `docs`
2. In GitHub Pages settings, select `/docs` as the source folder

## Local Preview

To preview the site locally, you can:

**Option 1: Python HTTP Server**
```bash
cd gh-pages
python -m http.server 8000
```
Then open http://localhost:8000

**Option 2: VS Code Live Server**
Install the "Live Server" extension and right-click `index.html` → "Open with Live Server"

## Customization

- **Update GitHub link**: Replace `YOUR_USERNAME` in `index.html` with your actual GitHub username
- **Add screenshots**: Place app screenshots in the `assets/` folder
- **Modify content**: Edit `index.html` for content and `style.css` for styling

## Files

- `index.html` - Main webpage
- `style.css` - Stylesheet
- `assets/` - Images and icons
  - `soteria.png` - App icon
