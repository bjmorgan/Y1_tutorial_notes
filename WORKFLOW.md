# Tutorial Preparation Workflow

This document describes the workflow for preparing tutorial notes using Claude Code. It is not part of the public-facing site.

## Quick start

Open the project in Claude Code and run:

```
/tutorial-prep <topic or path to materials>
```

This invokes the tutorial preparation skill, which walks through the five stages below.

## The five stages

### Stage 1: Review and interrogate the source material

Start with the tutorial questions and any provided notes or mark schemes. The goal is to work through each question together, understanding the underlying chemistry and physics.

**This is a conversation, not a document generation step.** Claude will read the material and give you a brief overview, then ask where you want to start. You work through the questions together: you explain what you think the key ideas are, ask questions about things you're less sure about, and discuss what students should take away. Claude should be a discussion partner, not a lecturer.

This is particularly important for topics you haven't taught recently or need to refresh your understanding of. The conversation is how you rebuild your own understanding before trying to explain it to students. Don't rush this stage.

### Stage 2: Draft tutorial notes (for you)

Based on the discussion, draft working notes for your own use in the tutorial. These capture the physical reasoning behind each question, common misconceptions to watch for, and key points to emphasise. These notes are informal and for your reference only.

### Stage 3: Review student submissions (optional)

If you have submitted student work, review it together. This identifies where students actually struggled (as opposed to where you predicted they would). The output is annotation suggestions for each student's work, draft feedback emails if wanted, and a list of topics the student-facing notes should address. Skip this stage if you don't have student work yet; you can come back to it later.

### Stage 4: Write student-facing notes

Write the conceptual reference notes as a bookdown chapter. These are informed by everything from the previous stages: your understanding of the physics, what you want to emphasise in the tutorial, and (if available) where students actually had difficulty. The notes explain why equations work, not just how to use them.

The output is an `.Rmd` file added to the bookdown project. See "Adding a new chapter" below.

### Stage 5: Publish

Build the site, check it renders correctly in all three themes (white, sepia, night), commit, and push. The GitHub Action handles deployment.

## How the stages connect

The workflow is sequential but iterative. You might go back to Stage 1 after seeing student work in Stage 3. You might revise the student notes after teaching the tutorial and discovering new points of confusion. The stages are a guide, not a rigid pipeline.

Not every tutorial needs all five stages. For a new tutorial with no student submissions yet, you would do Stages 1, 2, 4, and 5, then come back to Stage 3 after the tutorial.

## Project structure

```
TutorialNotes/
  CLAUDE.md                  # Project context for Claude Code (read automatically)
  WORKFLOW.md                # This file
  README.md                  # Public-facing README
  style.css                  # Shared CSS (theme-aware callout boxes)
  mathjax-mhchem.html        # Shared MathJax mhchem extension loader
  preamble.tex               # Shared LaTeX preamble for PDF output
  .claude/skills/            # Claude Code skills
  .github/workflows/         # GitHub Actions (builds both Y1 and Y2)
  Y1/                        # Y1 Physical Chemistry (CH12002)
    index.Rmd
    _bookdown.yml
    _output.yml
    01-ions-and-solutions.Rmd
    ...
  Y2/                        # Y2 Physical Chemistry (CH22008)
    index.Rmd
    _bookdown.yml
    _output.yml
    ...
```

Each year is an independent bookdown project. Shared resources (`style.css`, `mathjax-mhchem.html`, `preamble.tex`) live at the top level and are referenced via `../` paths in each year's `_output.yml`.

## Adding a new chapter

1. Create a new `.Rmd` file in the appropriate year directory (e.g. `Y1/04-thermodynamics.Rmd` or `Y2/01-electrochemistry.Rmd`)
2. Add it to the `rmd_files` list in that year's `_bookdown.yml`
3. Use `$\ce{...}$` for chemistry notation (rendered by MathJax mhchem)
4. Use `::: {.keypoint}` fenced divs for callout boxes (no "Key point:" prefix)
5. Avoid em dashes; use periods, commas, colons, or semicolons
6. Build and check all three themes

## Deployment

The sites are deployed via GitHub Pages. A GitHub Action builds both Y1 and Y2 on push to `main`, deploying to `.../Y1/` and `.../Y2/` respectively. Each year's `_site/` directory is gitignored.

## Files Claude Code uses

- **`CLAUDE.md`**: Project context that Claude reads automatically at the start of every session. Contains build instructions, file structure, and writing conventions. Edit this if the project structure or conventions change.
- **`.claude/skills/tutorial-prep/SKILL.md`**: The tutorial prep skill invoked by `/tutorial-prep`. Edit this if you want to adjust the workflow (e.g. add a stage, change the emphasis).

Both files are version-controlled and available on any machine where you clone the project.
