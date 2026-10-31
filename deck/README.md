# Beamer Template

A clean, reusable LaTeX Beamer deck (16:9, metropolis theme) with a
parameterised brand palette and a component cookbook.

## Structure

```
deck/
├── main.tex              <- the only file to edit for metadata
├── COMPONENTS.tex        <- preview/copy-paste slide library (not in the deck)
├── Preamble/
│   ├── preamble.sty      <- theme, packages, footer, section dividers
│   ├── branding.tex      <- colours + logo path
│   └── titlepage.tex     <- title slide (reads your metadata)
├── Sections/
│   ├── 00-agenda.tex     <- table of contents
│   ├── 01-section.tex    <- demo section, replace it
│   └── 99-thankyou.tex   <- closing slide
└── Assets/
    └── logo.png
```

## Quick start

1. Copy the whole `deck/` folder and rename it after your topic.
2. Open `main.tex` and fill in the five metadata lines:
   `\title`, `\subtitle`, `\author`, `\institute`, `\courseline`, `\date`.
3. Write your content in `Sections/` (see below) and delete the demo frames
   from `01-section.tex`.

## Branding

Everything visual lives in `Preamble/branding.tex`, in four lines:

```latex
\definecolor{BrandPrimary}{RGB}{36, 164, 220}
\definecolor{BrandAccent}{RGB}{201, 42, 135}
\definecolor{BrandDark}{RGB}{0, 33, 71}
\newcommand{\brandlogo}{Assets/logo.png}   % {} hides the logo
```

Change the RGB values and the whole deck follows (title card, section
dividers, frame titles, footer, links).

## Writing a section

Create `Sections/02-my-topic.tex`:

```latex
\section[Short title]{Long section title}

\begin{frame}{Slide title}
    \begin{itemize}
        \item Point
        \begin{itemize}
            \item Detail
        \end{itemize}
    \end{itemize}
\end{frame}
```

then add one line in `main.tex`:

```latex
\input{Sections/02-my-topic}
```

The `[Short title]` is what appears in the agenda, the section divider and the
footer, so keep it under ~40 characters. Do **not** put `\\` inside a section
title.

## Adding images

Put files in `Assets/` and reference them with the exact filename:

```latex
\includegraphics[width=0.7\linewidth]{Assets/diagram.png}
```

Filenames are **case-sensitive on Overleaf**, so `logo.png` and `Logo.png` are
different files. Use lowercase names without spaces.

## Building on Overleaf

1. Select the contents of `deck/` (not the folder itself) and zip them, so
   `main.tex` sits at the root of the zip.
2. In Overleaf: **New Project -> Upload Project**, choose the zip.
3. Leave the compiler on **pdfLaTeX** and `main.tex` as the main document.
4. Compile.

The metropolis theme ships with TeX Live on Overleaf, so no extra install is
needed. A local TeX distribution also works if you install `beamertheme-metropolis`.

## Previewing the components

Set `COMPONENTS.tex` as the main document in Overleaf to see every building
block (columns, figure, table, callouts, TikZ diagram, code listing, blocks,
statement slide, quote, closing). Copy any frame into `Sections/`, then switch
the main document back to `main.tex`.

## Vietnamese text

The template loads `babel` with English as the main language and Vietnamese
available. Occasional Vietnamese words work with pdfLaTeX. For a
predominantly Vietnamese deck, switch the Overleaf compiler to **XeLaTeX** and
replace the font block in `Preamble/preamble.sty`:

```latex
% remove these two lines
% \usepackage[utf8]{inputenc}
% \usepackage[T1]{fontenc}

% add this line
\usepackage{fontspec}
```

## The original deck

This template was cleaned from a 91-slide database-security presentation.
Git history keeps it intact:

```bash
git log --oneline            # 0d1b914 is the original import
git show 0d1b914 --stat      # list everything that was there
git checkout 0d1b914 -- .    # restore it into the working tree (careful)
```

A pdf of the original deck is also available at that commit, and the template
output can be compared against it if Overleaf ever reports a regression.

## Conventions

- One idea per slide; split instead of shrinking.
- Prefer `\section[short]{long}` and let the theme draw the divider.
- Prefer the global list spacing over `\vspace{-1.5cm}` hacks.
- Put figures in `Assets/`, sections in `Sections/`, nothing else at the root.
