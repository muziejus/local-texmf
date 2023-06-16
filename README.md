# Local texmf

Sometimes with LaTeX you want things installed globally, 
so you can always refer to them no matter where your writing project is.
That’s one of the use cases solved by using a local texmf tree;
anything in there is visible everywhere, 
and it’s where you would install niche packages.

It’s also a good place to stash boilerplate, like page margins,
a “default” set of packages, and so on.
Instead of having a long preamble that I have to copy from document to document,
like every week I have to submit a new homework assignment, 
I instead leverage texmf and create a “math-homework” LaTeX file that I 
`\input`. It, subsequently, refers to other documents in my local texmf to build
out the structure I want. 
On a per-document basis, I get a preamble less than 15 lines long, 
and whenever I want to update the look of my math homework,
I can do so for every math homework I have ever drafted.

So, then, this is my local texmf. On Macs, it’s installed in `~/Library/texmf`.

To my Overleaf friends, gl implementing something like this.

## Pandoc

The goal is to have these files legible both by vanilla LaTeX 
files and Pandoc files, which is an improvement on constructing a tree
of modular LaTeX files inside the Pandoc data tree 
(`~/.pandoc`, by default).

The way I do this is by rigidly enforcing and checking for set variables 
in the LaTeX files. That way, a vanilla LaTeX file might begin:

So, for example, a Pandoc template might begin:

```tex
\documentclass[letter,12pt,article,oneside]{memoir}

\newcommand{\mytitle}{My Awesome Title}
\newcommand{\myauthorname}{Moacir P. de Sá Pereira}
\newcommand{\myinputstemplate}{math-homework}

\input{\myinputstemplate}
```

The `math-homework` file is anticipating variables/commands 
called `\mytitle` and `\myauthorname`, so it can feed them into its own
headers, footers, and so on. 
In Pandoc, I have an interstitial template that converts Pandoc metadata
into LaTeX commands/variables, like this:

```tex
\documentclass[letter,12pt,article,oneside]{memoir}

\newcommand{\mytitle}{$title$}
\newcommand{\myauthorname}{$author.name$}
\newcommand{\myinputstemplate}{$inputs-template$}

\input{\myinputstemplate}
```

Here, `$title$`, `$author.name$`, and `$inputs-template$` refer 
to these metadata variables. 
See [Pandoc’s documentation on interpolated variables](https://pandoc.org/MANUAL.html#interpolated-variables) for more.

## Bibliographies

Part of the rationale for making my texmf folder a thing again 
after years of not using it is because it also stores, 
in `bibtex/bib`, a `.bib` file that contains my whole Zotero library.
What’s more, 
via [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/), 
the file is kept updated whenever I make a change to my Zotero library. 
This means the entire library is available to any 
LaTeX document I write, both just natively and via autocompletion.

The file is ignored in the git repo because there’s no point cluttering this repo with it, 
but I did flag the directories as a suggestion to future users,
including me, about leveraging this Zotero trick.

