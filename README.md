# NISMOD website

This is the technical site for NISMOD, the National Infrastructure Model
developed by [ITRC Mistral](http://www.itrc.org.uk/) (Infrastructure Transitions
Research Consortium, Multi-Scale Infrastructure Systems Analytics), supported by
EPSRC.

The first purpose of this site is to host training and reference material.

## Jekyll and Github pages

This repository is processed by [Github Pages](https://pages.github.com/)
to produce the site at [https://nismod.github.io/](https://nismod.github.io/)
using the [Jekyll](https://jekyllrb.com/) static site generator.

### Top level files

The `index.md` file corresponds to the home page of the site. Other markdown
files at the top level will be processed into pages on the site.

### Reference guides

Add a markdown file (`something.md`) to the `docs` directory to include a page
in the list of reference guides. These should use `layout: page` for default
styling.

### Presentations

Add a html file (`something-else.html`) to the `_presentations` directory with
content in markdown format to create a [`remark.js`](https://remarkjs.com/)
presentation.

To build and serve the site locally:

```bash
bundle exec jekyll serve
```

