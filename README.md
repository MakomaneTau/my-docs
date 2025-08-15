# my-docs

This is the documentation site for the **my-docs** project, built with [MkDocs](https://www.mkdocs.org) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme.

## Features

- Easy navigation with sidebar and search
- Responsive design
- Markdown-based content
- Built using MkDocs Material
- Supports code highlighting and diagrams
- Integrated with GitHub Pages for hosting
- Dark/light mode toggle
- Instant navigation and tabbed sections
- Copy and annotate code blocks
- Tagging and awesome-pages plugin support
- Git revision date display on pages

## Project Structure

```
mkdocs.yml         # MkDocs configuration file
docs/              # Source markdown files
site/              # Generated static site (after build)
README.md          # Project overview
images/            # Site logo and favicon
```

## Getting Started

1. **Install MkDocs and Material theme**  
   ```sh
   pip install mkdocs mkdocs-material
   ```

2. **Install extra plugins**  
   ```sh
   pip install mkdocs-awesome-pages-plugin mkdocs-minify-plugin mkdocs-git-revision-date-localized-plugin mkdocs-tags pymdown-extensions tzdata
   ```

3. **Serve Locally**  
   ```sh
   mkdocs serve
   ```
   Visit [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

4. **Build Static Site**  
   ```sh
   mkdocs build
   ```
   The output will be in the `site/` directory.

5. **Deploy to GitHub Pages**  
   ```sh
   mkdocs gh-deploy
   ```

## Documentation

- See [`docs/index.md`](docs/index.md) for the homepage.
- Add guides, references, and other documentation in the `docs/` folder.
- Organize content using Markdown files and update `mkdocs.yml` for navigation.

## Configuration Highlights

- **Theme:** Material with custom palette, logo, and favicon.
- **Navigation:** Multi-level sidebar, tabs, and instant navigation.
- **Plugins:** Search, tags, awesome-pages, git revision date, minify.
- **Markdown Extensions:** Admonition, code highlighting, tables, task lists, details, magic links, and more.
- **Extra:** Social links for GitHub and Twitter.

## Contributing

1. Fork the repository and clone locally.
2. Create a new branch for your changes.
3. Commit and push your changes.
4. Open a pull request on GitHub.

Feel free to open issues or submit pull requests.

## License

This project is licensed under the MIT License.

---

Made