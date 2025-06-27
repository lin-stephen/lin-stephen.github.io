# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site blog repository using the FixIt theme. The site is primarily written in Traditional Chinese (zh-tw) and serves as a technical blog with the title "操蟲師的獵人筆記" (Hunter's Notes of an Insect Master). The site is deployed to GitHub Pages automatically via GitHub Actions.

## Architecture

- **Static Site Generator**: Hugo (version 0.147.9)
- **Theme**: FixIt (located in `themes/FixIt/`)
- **Additional Themes**: PaperMod and faro-analytics as submodules
- **Content**: Blog posts stored in `content/posts/`
- **Configuration**: `hugo.yaml` (main site configuration)
- **Deployment**: GitHub Pages via `.github/workflows/hugo.yml`
- **Analytics**: Grafana Faro analytics integration

## Common Development Commands

### Local Development
```bash
hugo server -D
```
This starts the Hugo development server with draft posts enabled.

### Create New Post
```bash
hugo new content posts/<name-of-your-post>.md
```

### Build Site
```bash
hugo --minify
```
The built site will be output to the `public/` directory.

### Production Build (as used in CI)
```bash
hugo --minify --baseURL "<base-url>/"
```

## Site Configuration

The main configuration is in `hugo.yaml`:
- Base URL: https://lin-stephen.github.io/
- Language: Traditional Chinese (zh-tw)
- Theme: FixIt
- Analytics: Grafana Faro integration
- Menu structure includes categories (🗃️分類) and tags (🔖標籤)

## Content Structure

- Blog posts are stored in `content/posts/`
- Static assets for posts go in `static/assets/`
- The site uses Hugo's content organization with categories and tags

## Deployment

The site automatically deploys to GitHub Pages when changes are pushed to the main branch. The workflow:
1. Uses Hugo version 0.147.9
2. Installs Dart Sass for SCSS compilation
3. Builds with `--minify` flag
4. Deploys to GitHub Pages

## Theme Development

The FixIt theme includes its own package.json with build scripts, but the main site doesn't require npm/node dependencies for basic content creation and site building.