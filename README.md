# Adson Costanzi Filho — Blog

Personal blog about statistics, data science and R, built with [blogdown](https://pkgs.rstudio.com/blogdown/) (R + Hugo) and the [Hugo PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

- **Source of truth:** branch `source`
- **Deployed site:** branch `master` (GitHub Pages at <https://adsoncostanzifilho.github.io/>)
- **Languages:** English (default, at the site root), Portuguese (`/pt/`) and Spanish (`/es/`)

## Project structure

```
├── content/
│   ├── en/   # English posts (R Markdown) + pages (about, search)
│   ├── pt/   # Portuguese versions
│   └── es/   # Spanish versions
├── static/   # Images, CV and other static assets
├── themes/PaperMod   # Theme (git submodule)
├── hugo.toml         # Site configuration (Hugo ≥ 0.110)
├── .Rprofile         # blogdown global options
└── .github/workflows/blogdown.yaml  # CI: renders and deploys to master
```

## How to work on this blog

1. **Install Hugo** (pinned to the version in `.Rprofile`):

   ```r
   blogdown::install_hugo(extended = TRUE, version = "0.165.0")
   ```

2. **Create a new post** (English is the default language):

   ```r
   blogdown::new_post("My New Post", subdir = "blog")
   ```

   For the post to appear in all three languages, create translated versions of the
   R Markdown file under `content/pt/blog/` and `content/es/blog/` with the **same
   directory name** and the **same `slug`** (Hugo links them as translations).

3. **Serve locally** (with live reload):

   ```r
   blogdown::serve_site()
   ```

4. **Build**:

   ```r
   blogdown::build_site()
   ```

5. **Deploy:** push to the `source` branch. The GitHub Actions workflow
   (`.github/workflows/blogdown.yaml`) renders the site and publishes `public/`
   to the `master` branch, which GitHub Pages serves.

## Notes

- Posts are rendered with the blogdown **markdown method** (`blogdown.method = "markdown"`),
  so Hugo (Goldmark/Chroma) generates language-tagged code blocks
  (`<code class="language-r">`) with syntax highlighting. Images with a fixed
  width are written as raw `<img>` HTML in the sources (Goldmark drops the
  Pandoc `{width="70%"}` attributes).
- The `csgo-package` post executes R chunks that need `dplyr`, `tidyr`, `stringr`
  and `kableExtra`, and the `why-not-both` post executes Python chunks (via
  `reticulate`). The CI workflow installs these dependencies.
- Tags and categories are intentionally kept in English across all languages to
  keep the taxonomy unified.
