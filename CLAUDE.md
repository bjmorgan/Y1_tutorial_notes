# Tutorial Notes — Project Context

## What this project is

A monorepo containing two bookdown sites with student-facing tutorial notes at the University of Bath. The notes emphasise physical reasoning over rote equation application.

- **Y1/** — Y1 Physical Chemistry (CH12002)
- **Y2/** — Y2 Physical Chemistry (CH22008)

Each year is an independent bookdown project that builds to a separate site.

## How to build

```bash
cd /Users/benmorgan/Documents/Work/Teaching/TutorialNotes

# Build Y1
cd Y1 && Rscript -e 'bookdown::render_book("index.Rmd", "bookdown::gitbook")'

# Build Y2
cd Y2 && Rscript -e 'bookdown::render_book("index.Rmd", "bookdown::gitbook")'
```

Each year builds to its own `_site/` directory (gitignored). A GitHub Action builds both on commit and deploys to GitHub Pages at `.../Y1/` and `.../Y2/`.

## Project structure

```
TutorialNotes/
  CLAUDE.md                   # This file (shared project instructions)
  WORKFLOW.md                 # Workflow documentation
  README.md                   # Public-facing README
  style.css                   # Shared CSS (theme-aware keypoint boxes)
  mathjax-mhchem.html         # Shared MathJax mhchem loader
  preamble.tex                # Shared LaTeX preamble for PDF output
  .claude/                    # Claude Code skills
  .github/workflows/          # GitHub Actions (builds both sites)
  Y1/
    index.Rmd                 # Front matter and "About" page
    _bookdown.yml             # Chapter ordering and build config
    _output.yml               # Output format config (refs ../style.css etc.)
    01-ions-and-solutions.Rmd
    02-spectroscopy.Rmd
    03-kinetics.Rmd
  Y2/
    index.Rmd                 # Front matter and "About" page
    _bookdown.yml             # Chapter ordering and build config
    _output.yml               # Output format config (refs ../style.css etc.)
```

Shared resources (`style.css`, `mathjax-mhchem.html`, `preamble.tex`) live at the top level and are referenced from each year's `_output.yml` via `../` paths.

## Conventions

- **Chemistry notation**: use `$\ce{...}$` (mhchem via MathJax in HTML, mhchem package in LaTeX)
- **Callout boxes**: use `::: {.keypoint}` fenced divs. No "Key point:" prefix; the box styling is sufficient.
- **Tone**: supportive, not prescriptive. Present alternatives rather than saying "don't do X". The goal is to build understanding, not to dictate method.
- **Punctuation**: avoid em dashes. Use periods, commas, colons, or semicolons instead.
- **Content**: conceptual reference notes, not worked solutions to specific tutorial questions. Where worked examples are included, they should illustrate a general technique (e.g. Debye-Huckel calculation) rather than answer a specific question from the problem set.
- **CSS themes**: keypoint boxes have explicit colour definitions for all three gitbook themes (white, sepia, night). Do not use `currentColor`/`opacity` shortcuts.

## Git commits

- Do not include `Co-Authored-By` lines or other AI attribution in commit messages.

## Adding a new tutorial chapter

1. Create a new `.Rmd` file in the appropriate year directory (e.g. `Y1/04-thermodynamics.Rmd` or `Y2/01-electrochemistry.Rmd`)
2. Add it to the `rmd_files` list in that year's `_bookdown.yml`
3. Follow the conventions above
4. Use the `/tutorial-prep` skill to guide the preparation workflow
