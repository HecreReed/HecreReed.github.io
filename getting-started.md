---
title: Getting Started
layout: default
---

# Getting Started

Welcome to your new wiki! This guide will help you get started with creating and organizing your content.

## Creating New Pages

1. Create a new Markdown file in the `_docs` folder
2. Add front matter at the top:
   ```yaml
   ---
   title: Your Page Title
   layout: default
   ---
   ```
3. Write your content in Markdown

## Organizing Content

You can organize your wiki pages by:

- Creating subdirectories in `_docs/`
- Using categories in the front matter
- Creating an index page for each section

## Editing Content

1. Clone the repository: `git clone https://github.com/HecreReed/HecreReed.github.io.git`
2. Edit files locally
3. Commit and push changes
4. GitHub Pages will automatically rebuild your site

## Local Development

To preview your site locally:

```bash
bundle install
bundle exec jekyll serve
```

Then visit `http://localhost:4000` in your browser.

## Next Steps

- Customize the `_config.yml` file
- Add more pages to `_docs/`
- Explore different Jekyll themes
- Add navigation menus
