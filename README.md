# Beamer Template

A ready-to-use presentation template: 16:9 slides, HCMUT colours, a title slide
that fills itself in from six lines of text. Nothing to install — you edit the
text, upload the folder to Overleaf, and present.

---

## Use it in 4 steps

### 1. Download this project

On this page click the green **Code** button → **Download ZIP**, then unzip it
somewhere easy to find (for example your Desktop).

The presentation itself is inside the **`deck`** folder. That is the only folder
that matters.

### 2. Fill in the title slide

Open **`deck/main.tex`** in any text editor (Notepad, VS Code, or directly in
Overleaf later). The first block looks like this — replace the text between the
braces with yours:

```latex
\title{Presentation Title}
\subtitle{Optional subtitle}
\author{Your Name}
\institute{University -- Faculty}
\renewcommand{\courseline}{Course code -- Group X}
\date{\today}
```

Leave a line empty (`{}`) and it simply disappears. `\date{\today}` prints
today's date; write `\date{May 1, 2026}` to fix a date.

### 3. Write your slides

Every file in **`deck/Sections/`** is one part of the talk. `01-section.tex`
holds the demo slides — replace them with your own.

To add a new part of the talk, create a file such as `deck/Sections/02-results.tex`:

```latex
\section[Results]{Results and discussion}

\begin{frame}{What we measured}
    \begin{itemize}
        \item First point
        \item Second point
        \begin{itemize}
            \item A detail under it
        \end{itemize}
    \end{itemize}
\end{frame}
```

and add one line near the end of `main.tex`:

```latex
\input{Sections/02-results}
```

That is all. The agenda slide, the section divider and the footer update
by themselves, because they read the `\section[...]{...}` line.

> The text in `[...]` is what shows in the agenda and the footer — keep it
> short. Do not put `\\` inside a section title.

### 4. Zip it and upload it

1. Open the **`deck`** folder.
2. Select everything **inside** it (Ctrl + A).
3. Right-click → **Send to → Compressed (zipped) folder**
   (Windows 11: **Compress to ZIP file**).
4. Go to [overleaf.com](https://www.overleaf.com) → **New Project** →
   **Upload Project** → choose that zip.
5. Press **Recompile**. Done.

> **Check the zip before uploading:** double-click it. You should see
> `main.tex` immediately. If you only see a single `deck` folder, you zipped the
> folder instead of its contents — go back, open `deck`, and zip what is inside.

The compiler stays on **pdfLaTeX** and `main.tex` is already the main document,
so there is nothing to configure.

---

## What to change, and what to leave alone

| What you want to change | File |
|---|---|
| Title, subtitle, your name, university, course, date | `deck/main.tex` (top block) |
| Slides, text, sections | `deck/Sections/` |
| Colours and logo | `deck/Preamble/branding.tex` + `deck/Assets/logo.png` |
| Images used in slides | put them in `deck/Assets/` |
| Everything else (theme, fonts, footer) | `deck/Preamble/` — you can ignore it |

## Colours and logo

Open **`deck/Preamble/branding.tex`**. Four lines control the whole look:

```latex
\definecolor{BrandPrimary}{RGB}{36, 164, 220}
\definecolor{BrandAccent}{RGB}{201, 42, 135}
\definecolor{BrandDark}{RGB}{0, 33, 71}
\newcommand{\brandlogo}{Assets/logo.png}
```

Change the numbers, or drop your own picture into `deck/Assets/` as `logo.png`.
Set `\newcommand{\brandlogo}{}` to remove the logo.

## Adding images to a slide

Put the file in `deck/Assets/` and use its exact name:

```latex
\includegraphics[width=0.7\linewidth]{Assets/diagram.png}
```

Names are **case-sensitive** on Overleaf: `logo.png` and `Logo.png` are different
files. Use lowercase, no spaces.

## Need a slide pattern?

`deck/COMPONENTS.tex` is a collection of ready-made slides: two columns, a big
figure, a table, callout boxes, a flow diagram, code, blocks, a quote, a closing
slide. Open it on Overleaf (set it as the main document) to see them, then copy
the frames you want into `Sections/`.

## If something goes wrong

- **`File not found` for an image** — the filename in the zip differs in case or
  spelling from what you typed.
- **The zip opens into a folder instead of `main.tex`** — see the check in step 4.
- **Vietnamese letters look wrong** — switch the Overleaf compiler to
  **XeLaTeX** (Menu → Compiler) and follow the note at the top of
  `Preamble/preamble.sty`.
- **Text spills off a slide** — split it into two slides instead of shrinking
  the font.

## For reference

This template came from a 91-slide database-security presentation; the untouched
original is kept in the git history (`git show 0d1b914 --stat`) in case you ever
want to compare.

Slides read best with one idea per frame, and section dividers left to the theme
rather than made by hand.
