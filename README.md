# wiki
The wiki page of my personal website

Built with [Zensical](https://zensical.org) and styled to match [alimahani.com](https://alimahani.com). It is served at [wiki.alimahani.com](https://wiki.alimahani.com).

## Preview locally

```bash
pip install -r requirements.txt
zensical serve                  # http://localhost:8000
zensical build --strict --clean # the same build CI runs
```

Pushing to `main` builds the site and deploys it to Cloudflare with `wrangler deploy` (see `wrangler.jsonc`).

## Where the theme lives

- `docs/stylesheets/extra.css` has the colors, fonts and component styles for the `classic` variant. The tokens at the top copy `website/src/styles/global.css`.
- `overrides/` holds the template changes: the header, the page header with description and reading time, the footer links, and `home.html` for the landing page.
- A page's `description` front matter shows under its title and in the list on the home page.
- Zensical renders templates with minijinja, not Jinja2. There is no `wordcount` filter, no `now()` and no Python string methods such as `.split()`. Use filters like `split` and `striptags` instead.
- The footer year is in `copyright` in `zensical.toml`. Update it each January.
