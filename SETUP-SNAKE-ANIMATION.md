# 🐾 Setup Animated Contribution Creature

To get the animated contribution creature working on YOUR GitHub profile, follow these steps:

## Step 1: Create GitHub Action Workflow

1. In your **profile repository** (the repo named `ankitaa19` - same as your username), create this folder structure:
   ```
   .github/workflows/
   ```

2. Create a new file: `.github/workflows/snake.yml`

3. Add this code to the file:

```yaml
name: Generate Snake

on:
  schedule:
    - cron: "0 */12 * * *" # Runs every 12 hours
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ankitaa19
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
            dist/ocean-contribution-grid.svg?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9

      - name: Push snake to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Step 2: Update Your README

Once the GitHub Action runs successfully, update your README.md to use YOUR contribution snake:

Replace:
```markdown
<img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/platane/platane/output/github-contribution-grid-snake.svg">
```

With:
```markdown
<img alt="github contribution grid snake animation" src="https://raw.githubusercontent.com/ankitaa19/ankitaa19/output/github-contribution-grid-snake-dark.svg">
```

## Step 3: Trigger the Action

1. Go to your repository on GitHub
2. Click on "Actions" tab
3. Click on "Generate Snake" workflow
4. Click "Run workflow" button
5. Wait for it to complete (takes ~1 minute)

## Customization Options

You can customize your creature by modifying the `color_snake` and `color_dots` parameters:

- **color_snake**: Changes the creature's color (e.g., `orange`, `#FF6B6B`, `purple`)
- **color_dots**: Changes the contribution dot colors (5 colors for different contribution levels)

### Fun Themes:

**Ocean Theme:**
```yaml
color_snake=blue&color_dots=#d0e8ff,#7cb3ff,#4a8fff,#266bff,#0047e1
```

**Sunset Theme:**
```yaml
color_snake=orange&color_dots=#fff4d6,#fec97a,#fe9b4a,#fd6d21,#f94c00
```

**Forest Theme:**
```yaml
color_snake=green&color_dots=#d6f5d6,#9edf9e,#67c767,#3cb043,#1a8b2f
```

## Troubleshooting

- **Action fails?** Make sure you have a repo named exactly `ankitaa19` (your username)
- **Snake not showing?** Wait 5-10 minutes after first run, GitHub needs time to generate images
- **Wrong contributions?** The snake uses your actual GitHub contributions, not just one repository

Enjoy your animated contribution creature! 🎉🐍🐾
