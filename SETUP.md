# Dipam Jha — GitHub Profile Setup

Customized for **DipamJha** with a green AI/ML and software-engineering theme.

## 1. Create the profile repository
Create a **public** GitHub repository named exactly `DipamJha` under the `DipamJha` account: `https://github.com/DipamJha/DipamJha`. GitHub displays this repository's README on your profile.

## 2. Review the content
- `README.md`: profile layout, contact links, skills, projects, and achievements.
- `assets/skills.json`: illustrative self-rated skill values (0–100); adjust them to your actual proficiency.
- `assets/projects.json`: featured repository slugs. Verify the repo names exist under your account and edit any that differ.
- `.github/workflows/`: automation for metrics, charts/cards, and contribution snake.

Email and LeetCode are set to the details supplied. Portfolio is omitted. LinkedIn is set to `https://www.linkedin.com/in/dipam-jha/`; update it if needed.

## 3. Push the files
Extract the ZIP and run from its folder:

```bash
git init
git branch -M main
git add .
git commit -m "Add customized GitHub profile"
git remote add origin https://github.com/DipamJha/DipamJha.git
git push -u origin main
```

If you already cloned the profile repository, copy these files into that clone and commit/push rather than running `git init`.

## 4. Enable Actions write access
Repository **Settings → Actions → General → Workflow permissions** → select **Read and write permissions** → Save. This allows workflows to commit generated SVGs and publish the snake animation.

## 5. Add the metrics token
The Metrics workflow expects an Actions secret named `METRICS_TOKEN`.
1. Create a GitHub personal access token at https://github.com/settings/tokens. Use only scopes required for the metrics you want (`read:user` for public profile data; `repo` only if including private repository data).
2. In your profile repo, open **Settings → Secrets and variables → Actions → New repository secret**.
3. Name it `METRICS_TOKEN` and paste the token. Never commit the token or put it in README.

Without this secret, metrics may fail or be incomplete.

## 6. Run the workflows
Open **Actions**, enable workflows if prompted, then use **Run workflow** for Metrics, Snake, and Charts and cards. Snake images may not appear until the Snake workflow succeeds once and creates the `output` branch. Scheduled workflows refresh generated assets afterward.

## 7. Optional local generation
Python 3.12 is recommended:

```bash
python scripts/radar.py --data assets/skills.json -o assets/radar
python scripts/radar.py --github DipamJha -o assets/radar-langs --limit 7 --values --curve 0.4 --exclude "shell,makefile,dockerfile,batchfile,procfile"
python scripts/cards.py --user DipamJha --projects assets/projects.json --out assets
```

## Notes
- Keep the repository public for relative SVG assets to render.
- Project links assume the slugs in the README are accurate; verify them before publishing.
- GitHub contribution charts represent GitHub activity, not all coding activity.
- The skill radar is self-assessed, not an independently measured score.
- The previous owner's portrait assets have been removed.


## Animated profile portrait

`assets/portrait.svg` is generated from the photo you supplied, using the template's colour dot-matrix rendering and staggered row-by-row reveal animation. The original photo is not included in this ZIP.

To regenerate it with a different image, save your photo locally as `me.jpg` and run from the repository root:

```bash
python -m pip install Pillow
python scripts/dotify.py me.jpg -o assets/portrait --cols 100 --equalize --detail 0.5 --color --reveal
```

The generated SVG is referenced near the top of `README.md`. GitHub may not play SVG CSS animations in every context or client; check the rendered profile after pushing.
