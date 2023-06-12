# USFDissertationTemplate
An unofficial template to mostly meet USF's ETD guidelines

#### Table of Contents  
- [Description](#description)
- [Getting Started](#getting-started)
  - [Class Options](#class-options)
  - [Title Page](#title-page) 
  - [Preamble](#preamble)
    - [Packages](#packages)
    - [Macros](#macros) 
    - [Formatting](#formatting)
  - [Main Body](#main-body)
  - [Bibliograph](#bibliography)
- [Some Style Tips](#some-style-tips)

## Description
The project can be copied (and viewed) from [Overleaf](https://www.overleaf.com/read/qmrvgskkzrmr). Though a lot of time and effort went into making this document meet ETD guidelines in Summer 2022 it is bound to 
* have missed some formatting requirements
* become outdated when requirements change
* produce documents that meet the requirements but still get flagged by ETD reviewers (looking at you, "half empty" spaces that are _less_ than 5.5" long)
It falls on the user to do several checks before submitting. A checklist is provided, though it may not be exhaustive. 

This template was written to be used "right out of the box," with sample files that can be readily modified and code snippets that can be adapted as necessary. Many useful packages have already been loaded, both in the `.cls` file (mostly formatting that may break if messed around with too much) and in the preamble file. Be wary of the order in which you add packages to the preamble. For example, `cleveref` can produce errors when it is not the last package to be loaded. Generally, for the less $\LaTeX$ savvy it may be best to add new macros and packages in the neighborhood of other things in the template that are serving a similar purpose.

Should you run into a problem not easily answered by web searches or the kind people of [stackexchange](https://tex.stackexchange.com/) just submit an issue and I'll see what I can do about it. 

## Getting Started
The project is organized as a series of separate files (`.tex`, `.bib`, plus the `.cls` file defining the document class), called when necessary in `main.tex`. Images and Tikz code files have their own separate folders. The suggested use is to have one `.tex` file for each chapter (or chapter like) section, with the exception of the acknowledgments and dedication (since those tend to be short and go together). 

### Class Options
If you have strong feelings about formatting, a few options have been made available. Namely, you can change the font size (`10pt`, `11pt` and `12pt`) and the style of chapter headings (`boldheadings`, `boldcaps`, `allcaps` and `plainheadings`). You can load them in the first line of `main.tex`

``` latex
\documentclass[10pt, boldcaps]{USFDissertation}
```

### Title Page 
All the information here is used to create the title page and add some metadata to the .pdf (so that .pdf readers can see the title and author). Make sure to check that the degree you type in is exactly as listed in the USF catalog and that you comment out anything you don't need. You do not need to manually separate long titles to add an empty line, this is done for you by the template. Note that $\LaTeX$ interprets consecutive nonempty lines of code as part of the same text, so that even if you write the title in multiple lines it will only force a line break where needed. The `\title` command doesn't like actual line breaks, though, so don't separate the text with empty lines. If you forget to use Title Case in your title, the class will do it for you. If this results in capitalizing a word that should not be capitalized, this can be fixed in the preamble. 

Typing in
``` latex
# See how the title content can be broken after `Can be Two Lines' but it 
# actually breaks in the PDF after `Exceed Two Lines'
\title{The title of the tanuscript Must be in Title Case: It Can be Two Lines, 
but Cannot Exceed Two Lines - If Two Lines Make Sure to Add a Space}
\author{Author Name}
\def\mydegree{Doctor of Philosophy}
\def\mydepartment{Mathematics \& Statistics}
\def\mycollege{Arts and Sciences}
```
Results in 

<img width="509" alt="titlepage" src="https://github.com/fajardogomez/USFDissertationTemplate/assets/109635630/df3f656e-8f4d-436b-b9f5-6f4b6d907221">

### Preamble
Here is where packages are loaded and you can define your own macros (i.e. you can add your own commands/environments).

#### Packages
Some commmonly used packages for mathematics are included already, so you don't need to add them again.  Keep in mind that these are called from `\input{preamble}` in `main.tex` so it's better not to add any more packages before `\begin{document}` there to avoid compatibility issues. The file `preamble.tex` includes packages you will likely need:
``` latex
# Useful packages for math papers
\usepackage{mathtools}
\usepackage{amsmath, amsthm, amssymb, amsfonts, amsopn, bm, bbm}

# Creates the bibliography
\usepackage[style=numeric,sortcites]{biblatex}
\addbibresource{biblio.bib}

# Unlike \ref, \cref automatically detects environments. 
\usepackage[noabbrev,capitalize]{cleveref}
```
Note that `cleveref` is loaded near the end of the file. To be safe, check that the pacakges you want are not already included in the preamble (otherwise you may end up loading them twice wtih conflicting settings), and add packages near the top of the preamble file (where `mathtools` is loaded). 

#### Macros
If you find yourself typing the same symbols or combinations of symbols over and over again, it's worth adding them in the preamble as commands. Takes a lot less time to type `\N` than `\mathbb{N}` to print $\mathbb{N}$. 
``` latex
\newcommand{\N}{\mathbb{N}}
\newcommand{\Z}{\mathbb{Z}}
\newcommand{\R}{\mathbb{R}}
\newcommand{\tinfty}{\rightarrow \infty}
```
Commands can also take arguments. The number of arguments is indicated in between square brackets (if you need more, change `[1]` for `[2]` or whatever you need and insert `#2`, `#3`, etc where the argument is used). The command below lets us type `\seq{x}` to print $\left( x_n \right)_ {n \in \mathbb{N}}$. 
``` latex
\newcommand{\seq}[1]{\left(#1_n\right)_{n \in \N}}
```
You can also use commands to print comments in the .pdf file (which is nice if you prefer to read from there as opposed to using Review in Overleaf). There is a built in command for this:
``` latex
\newcommand{\PersonA}[1]{{\color{#2081F7}\textbf{Person A says:} #1}}
```
which prints `\PersonA{hi}` as ${\color{#2081F7}\textbf{Person A says:}\text{ hi}}$. You can add more and change the colors if you're getting feedback from more than one advisor.

You may also find it useful to define delimiters and operators. Besides being faster to type, the delimiter `\abs` also automatically resizes. If you were using `|x|` before, note that it doesn't play nice with larger symbols, and `|\displaystyle\sum_{i=1}^\infty x_i|` just doesn't look quite right $|\displaystyle\sum_{i=1}^\infty x_i|$. You could use `\left|\displaystyle\sum_{i=1}^\infty x_i\right|`, which results in $\left|\displaystyle\sum_{i=1}^\infty x_i\right|$. The faster way of getting the same results with the macro is to use the starred version of `\abs`: `\abs*{\displaystyle\sum_{i=1}^\infty x_i}`. Though some ooperators are already defined, the typesetting of `$\sin x$` ($\sin x$) is different from what you'd get using `$\text{sin} x$` ($\text{sin} x$) and not all the operators you'd want are necessarily built in. 
``` latex
\DeclarePairedDelimiter\abs{\lvert}{\rvert}
\DeclarePairedDelimiter\ceil{\lceil}{\rceil}
\DeclarePairedDelimiter\floor{\lfloor}{\rfloor}
\DeclareMathOperator{\sign}{sign}
```
Theorems, propositions, definitions, etc. are also included in the preamble. You can tweak the settings a bit if you don't like them or want to rename anything. All of them are are counted per chapter, and use the same counter (so that you don't have both Theorem 1.23 and Definition 1.23 but Theorem 1.23 and Definition 1.24). This is adjusted with the optional `[Thm]` in the definitions. The styles are either the default theorem or definition styles in the `amsmath` package. You can use `\theoremstyle` to modify this further, but the reviewers have been known to interpret these environments as higher order headings and don't like to see them with different styles.
``` latex
\newtheorem{Thm}{Theorem}[chapter]
\newtheorem{Coro}[Thm]{Corollary}
\newtheorem{Prop}[Thm]{Proposition}
\newtheorem{Lem}[Thm]{Lemma}
\newtheorem{Conj}[Thm]{Conjecture}
\newtheorem{Prob}[Thm]{Problem}
\theoremstyle{definition}
\newtheorem{Def}[Thm]{Definition}
\newtheorem{Ex}[Thm]{Example}
\newtheorem{Rmk}[Thm]{Remark}
\newtheorem{Note}[Thm]{Notation}
```
You can add short titles in square brackets (useful for named theorems) and labels so that you can reference these later. 
``` latex
\begin{Thm}[Theorem name]
\label{mythm}
This is a theorem.
\end{Thm}
```
#### Formatting
The class file does a lot of the heavy lifting for you: it's written to automatically write sections and chapters using Title Case, so you can use sentence case everywhere. However, if you notice anything that doesn't look quite right, you can add words here 
``` latex
% List of words that will not be capitalized in Title Case
\Addlcwords{of, and, a, an, the, or, to, in, on, at}
```
so that they are not capitalized. While you can use math symbols (and math mode in general) in headings and chapter/section/subsection titles, they will automatically capitalize. So that if you wanted something like $(p,q)$ as part of a section title, which will print as $(P,q)$ with the current settings in the Table of Contents, you'll have to add the entire expression `$(p,q)$` to `\Addlcwords` so that it prints correctly.

The `hyperref` package is loaded for you, with an option to make hyperlinks dark blue. You can comment out the package altogether to get rid of links or change the color of the hyperlinks to anything you like. Anecdotally, reviewers don't like to see color text so you can save yourself a round of revisions by just setting them to black (`{rgb}{0,0,0}`) here:
``` latex
\usepackage[dvipsnames]{xcolor}
\definecolor{pdflinkcolor}{rgb}{.1,.1,.6}	% darkblue
\definecolor{pdfcitecolor}{rgb}{.6,.1,.1}	% darkred
\definecolor{pdfanchorcolor}{rgb}{0,1,0}	% green
\definecolor{pdfurlcolor}{rgb}{.1,.6,.1}	% darkgreen
\definecolor{pdfpagecolor}{rgb}{0,0,1}	 % blue
\definecolor{pdffilecolor}{rgb}{1,0,0}	 % red
```
### Main Body
Once you're done writing an abstract (in `abstract.tex`) you can move on to the chapters, each in their own `chapter<n>.tex` files. A few things to keep in mind:
1. Though the class saves vertical space in the right places for table and figure captions, it will be up to you to make sure to include the `\caption` commands in the appropriate place. That is, you should put table captions _before_ the tables and figure captions _after_ the figures.
2. When you write captions, use the syntax `\caption[<First sentence only.]{<Full caption.>}`. This ensures that anything between the square brackets gets printed on the List of Tables and List of Figures (which should only be the first sentence and not the whole caption). 
3. Use sentence case throughout for titles, no matter what level (i.e. chapter, section, subsection, etc.). The formatting is done for you by the class file.
4. Use `\Cref{mythm}` instead of `Theorem~\ref{mythm}` when referencing theorem-like environments like the one defined above. The package `cleveref` will check the environment and add its name for you. That way, if later down the line you decide that the result is not as big of a deal and you want to demote it to proposition, you can change the code to 
``` latex
\begin{Prop}[Theorem name]
\label{mythm}
This is a theorem.
\end{Prop}
```
without having to track down every instance of `\Cref{mythm}` and changing it. If you'd used `Theorem~\ref{mythm}`, you'd have to manually change every instance to `Proposition~\ref {mythm}`. 
5. Use `\Cref` or `\cref` consistently: one will print "Theorem 1.23" while other will print "theorem 1.23"). 

### Bibliography
The file `biblio.bib` is included in the template. You can type in (or copy and paste) BibTeX entries there. Just make sure to skim through any you don't manually type in to make sure they have all the information correct. Type out author names in full (often Google Scholar results only show the first initial), separate the given and family name with commas (`Family Name, Given`) if you're worried they will print incorrectly (i.e. "Given F. Name" for the example given). 

## Some Style Tips
1. Add punctuation at the end of equations if they are used as part of a sentence.
2. Don't start sentences with references or notation (e.g. "The set of real numbers is denoted by $\mathbb{R}$" instead of "$\mathbb{R} denotes the set of real numbers.")
3. Use `\begin{sloppypar}` and `\end{sloppypar}` to enclose paragraphs with in-line math that runs off the margins.
For more, read the first chapter of [A Primer of Mathematical Writing](https://arxiv.org/pdf/1612.04888.pdf).
