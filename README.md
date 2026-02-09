# My Wiki

Personal knowledge base and documentation powered by Jekyll and GitHub Pages.

## 🚀 Quick Start

Visit the wiki at: https://HecreReed.github.io

## 📝 Adding Content

1. Create new Markdown files in the `_docs/` directory
2. Add front matter to each file:
   ```yaml
   ---
   title: Your Page Title
   layout: default
   ---
   ```
3. Commit and push changes
4. GitHub Pages will automatically rebuild the site

## 🛠️ Local Development

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# Visit http://localhost:4000
```

## 📚 Structure

```
.
├── _config.yml          # Site configuration
├── _docs/               # Wiki content
│   ├── getting-started.md
│   ├── changelog.md
│   └── index.md
├── index.md             # Homepage
├── Gemfile              # Ruby dependencies
└── README.md            # This file
```

## 🎨 Customization

Edit `_config.yml` to customize:
- Site title and description
- Theme (try `minima`, `jekyll-theme-cayman`, or `just-the-docs`)
- Navigation and collections

## 📖 Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Markdown Guide](https://www.markdownguide.org/)
