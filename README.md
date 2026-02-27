# CH12002 Tutorial Notes

Student-facing tutorial notes for Y1 Physical Chemistry at the University of Bath. Built with [bookdown](https://bookdown.org/).

The live site is at: *(add your GitHub Pages URL here)*

## What these notes are

Conceptual companion notes for the tutorial problem sets. They aim to help students understand the physical reasoning behind the calculations, rather than just applying equations by rote.

These are not worked solutions to the tutorial questions. They are reference notes that explain the underlying chemistry.

## Building locally

You need R and the `bookdown` package installed.

```bash
Rscript -e 'bookdown::render_book("index.Rmd", "bookdown::gitbook")'
```

Output goes to `docs/`. Open `docs/index.html` in a browser to preview.

## Writing conventions

- **Tone**: supportive, not prescriptive. Present alternatives rather than telling students what not to do.
- **Content**: explain the physics behind equations. Worked examples illustrate general techniques, not solutions to specific tutorial questions.
- **Chemistry notation**: `$\ce{NaCl}$`, `$\ce{H2O}$`, etc. (rendered by MathJax with mhchem)
- **Callout boxes**: use `::: {.keypoint}` fenced divs in the `.Rmd` files.
