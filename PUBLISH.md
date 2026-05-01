# How to publish this repo to GitHub

Step-by-step from "folder on my laptop" → "private repo on GitHub" → "public + GitHub Pages" when you're ready.

---

## 1. One-time: install and authenticate `gh` (recommended)

The GitHub CLI makes this much easier than the web UI.

**macOS:**
```bash
brew install gh
gh auth login        # follow prompts; pick GitHub.com, HTTPS, browser auth
```

**Windows:** `winget install --id GitHub.cli` then `gh auth login`
**Linux:** see https://github.com/cli/cli#installation

Verify:
```bash
gh auth status
```

---

## 2. Initialise the repo locally

From the workshop folder:

```bash
cd path/to/neurodesk-ms-workshop
git init
git add .
git commit -m "Initial workshop scaffold"
```

---

## 3. Create the **private** GitHub repo and push

```bash
gh repo create neurodesk-ms-workshop \
  --private \
  --source=. \
  --remote=origin \
  --push
```

That's it — your private repo is up at `https://github.com/<your-username>/neurodesk-ms-workshop`.

### If you don't want to use `gh`

Create the repo manually at https://github.com/new (set it to Private), then:
```bash
git remote add origin https://github.com/<your-username>/neurodesk-ms-workshop.git
git branch -M main
git push -u origin main
```

---

## 4. Day-to-day: developing the workshop

Standard git workflow:
```bash
git add .
git commit -m "Add lesion segmentation example"
git push
```

Useful while you build slides:
- Use `git lfs` if PPTX files get large (>50 MB):
  ```bash
  brew install git-lfs
  git lfs install
  git lfs track "*.pptx" "*.pdf"
  git add .gitattributes
  ```
- Keep `data/` empty in the repo — `.gitignore` already blocks `*.nii.gz`.

---

## 5. When ready: flip to public + enable GitHub Pages

A few days before the workshop:

### Make the repo public
```bash
gh repo edit --visibility public --accept-visibility-change-consequences
```

Or in the web UI: Settings → General → "Change visibility" at the bottom.

> **Last check before going public:** ensure no patient data, credentials, or unpublished slides have slipped in. Run `git log --all -- '*.nii.gz' '*.dcm'` to confirm nothing imaging-related is in history.

### Enable GitHub Pages
Easiest via the web UI — `gh` doesn't fully cover Pages config:

1. Go to repo **Settings → Pages**
2. **Source:** Deploy from a branch
3. **Branch:** `main`, folder `/ (root)`
4. Save

Within ~1 minute the site is live at:
```
https://<your-username>.github.io/neurodesk-ms-workshop/
```

The `_config.yml` in this repo applies the Cayman theme automatically. Edit it to change the title, theme, or excluded paths.

### CLI alternative for Pages

```bash
gh api repos/:owner/neurodesk-ms-workshop/pages \
  -X POST -f source[branch]=main -f source[path]=/
```

---

## 6. After the workshop

Useful follow-ups:
- Tag a release: `gh release create v1.0 --title "Workshop YYYY-MM-DD" --notes "..."`
- Add a CONTRIBUTING.md if you want attendees to send back fixes
- Pin the Neurodesk image tag in `setup/README.md` to the version you actually used during the workshop, for reproducibility

---

## Sanity checklist

- [ ] `git status` is clean
- [ ] `.gitignore` is committed and excludes `*.nii.gz`
- [ ] No credentials, API keys, or patient identifiers in any committed file
- [ ] README.md renders correctly on GitHub
- [ ] Slides PDF added before workshop date
- [ ] Visibility flipped to public ≥24 h before workshop (Pages can take a few minutes to first-build)
