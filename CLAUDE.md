# CLAUDE.md

## Project Overview

GitHub Profile README for [rommelporras](https://github.com/rommelporras). This repository name must match the GitHub username exactly for the README to render on the profile page.

## Repository Structure

```
rommelporras/
├── CLAUDE.md                       # This file
├── README.md                       # Profile README (renders on github.com/rommelporras)
└── .github/
    └── workflows/
        ├── snake.yml               # Daily snake animation generation (Platane/snk)
        └── blog-posts.yml          # Auto-pull latest blog posts from RSS
```

## Widget Services

| Widget | Service URL | Theme |
|--------|------------|-------|
| Typing animation | readme-typing-svg.demolab.com | Dark |
| Skill icons | skillicons.dev | Dark |
| GitHub Stats | github-profile-summary-cards.vercel.app | github_dark |
| Streak Stats | github-readme-streak-stats-eight.vercel.app | github-dark-blue |
| Trophies | github-trophies.vercel.app | darkhub |
| Activity Graph | github-readme-activity-graph.vercel.app | github-dark |
| Profile Views | komarev.com/ghpvc | flat-square |
| Snake Animation | Platane/snk@v3 (GitHub Action) | github-dark |
| Blog Posts | Custom curl + feedparser (GitHub Action) | N/A |

## Automation

### Blog Posts (blog-posts.yml)

- **Schedule:** Daily at midnight UTC
- **Source:** RSS feed from `blog.rommelporras.com/rss/`
- **Max posts:** 5
- **How it works:** curl fetches RSS, Python feedparser parses it, updates README between `<!-- BLOG-POST-LIST:START -->` and `<!-- BLOG-POST-LIST:END -->` markers
- **Cloudflare dependency:** Requires Bot Fight Mode OFF and WAF Rule 1 to skip Super Bot Fight Mode (see homelab docs/context/ExternalServices.md)

### Snake Animation (snake.yml)

- **Schedule:** Daily at midnight UTC
- **How it works:** Platane/snk@v3 generates SVGs from the GitHub contribution graph
- **Output:** Pushes `github-snake.svg` and `github-snake-dark.svg` to the `output` branch
- **Referenced in README via:** `https://raw.githubusercontent.com/rommelporras/rommelporras/output/github-snake-dark.svg`

## Common Tasks

### Manually trigger workflows

```bash
cd ~/personal/rommelporras
gh workflow run blog-posts.yml    # Update blog posts now
gh workflow run snake.yml         # Regenerate snake animation
```

### Check workflow status

```bash
cd ~/personal/rommelporras
gh run list --limit 5
```

### Add a new tech stack icon

Edit `README.md` — find the `skillicons.dev` URLs and add the icon name. Available icons: https://skillicons.dev

### Change typing animation text

Edit the `lines=` parameter in the `readme-typing-svg.demolab.com` URL. Use `+` for spaces and `%7C` for `|`. Preview at: https://readme-typing-svg.demolab.com/demo/

### If a widget breaks (shows broken image)

Community Vercel instances go down frequently. Check the service URL directly in a browser. If down, find an alternative mirror or self-host by forking the original repo and deploying to your own Vercel.

## How to Test

Push changes to `main` branch, then visit https://github.com/rommelporras to see the rendered profile.

## Related

- Homelab repo: https://github.com/rommelporras/homelab
- Blog: https://blog.rommelporras.com
- Portfolio: https://rommelporras.com
- Cloudflare WAF rules: homelab → docs/context/ExternalServices.md
