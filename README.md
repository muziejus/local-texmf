# Local texmf

This is my local texmf. On Macs, it’s installed in `~/Library/texmf`.

All the files here will be visible to LaTeX and friends,
regardless of whether LaTeX is invoked by Pandoc or by itself.
This is an improvement on my old system of stashing LaTeX files 
in Pandoc’s folder.

The way this works for LaTeX files is that all of my little settings
are broken up into various files that LaTeX/Pandoc `\input`s. 
Pandoc reads in variables from the metadata, 
which are converted into LaTeX in the base document, 
and which are subsequently fed to these files. 

So, for example, a Pandoc template might begin:

```tex
\documentclass[letter,12pt,article,oneside]{memoir}

\newcommand{\mytitle}{$title$}
\newcommand{\myauthorname}{$author.name$}
\newcommand{\myinputstemplate}{$inputs-template$}

\input{\myinputstemplate}
```

Here, `$title$`, `$author.name$`, and `$inputs-template$` refer to metadata variables. See [Pandoc’s documentation on interpolated variables](https://pandoc.org/MANUAL.html#interpolated-variables) for more.

However, in vanilla LaTeX, we might have:

```tex
\documentclass[letter,12pt,article,oneside]{memoir}

\newcommand{\mytitle}{My Awesome Title}
\newcommand{\myauthorname}{Moacir P. de Sá Pereira}
\newcommand{\myinputstemplate}{math-lecture-notes}

\input{\myinputstemplate}
```

The title and author’s name need to be filled in.

But in both cases, there are now available `\mytitle`,  `\myauthorname`, and `\myinputstemplate` which can be accessed by the various subsequent files that are `\input`ed via the value of `\myinputstemplate`.

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

