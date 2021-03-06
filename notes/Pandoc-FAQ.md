# Pandoc FAQ

### Turning off hyphenation

http://tex.stackexchange.com/questions/5036/how-to-prevent-latex-from-hyphenating-the-entire-document

you can use \usepackage[none]{hyphenat} to select a 'language' with no hyphenation at all. This works fine for a single language document, but not if you want to use babel or polyglossia for other language-specific effects.

Produces: 

pandoc: Error producing PDF from TeX source

Note: Pandox, when using Xetex, uses the polyglossia package for hyphenation.
http://ctan.org/pkg/polyglossia

Solution: use this rule:

\hyphenrules{nohyphenation}

Note: it must be declared after the Polyglossia package has been loaded. Declaring it at line 250 works fine.

### Styling chapter titles

https://www.sharelatex.com/learn/Sections_and_chapters

titleformat 

\titleformat
{<command>}
[<shape>]
{<format>}
{<label>}
{<sep>}
{<before-code>}
[<after-code>]


where [<shape>] and [<after-code>] are optional parameters, and:

<command> is the sectioning command to be redefined: \part, \chapter, \section, \subsection, \subsubsection, \paragraph or \subparagraph.
<shape> is sectioning paragraph shape; possible values are: hang, block, display, runin, leftmargin, rightmargin, drop, wrap, frame.
<format> is the format to be applied to the title, label, and text; for example \normalfont\Large\bfseries
<label> specify sectioning label.
<sep> is the horizontal separation between label and title body and it must be a length and not be empty.
<before-code> is code preceding the title body.
<after-code> is code following the title body.

### Set fonts

To set document-wide fonts, use \setmainfont, \setsansfont and \setmonofont.

Also, setromanfont

Available sizes:

\tiny
\scriptsize
\footnotesize
\small
\normalsize
\large
\Large
\LARGE
\huge
\Huge

### Allow long URLs to break

Long URLs will break at the end of line if they contain a hyphen, otherwise they won't break.

Workaround:

Use the [zero-width space](https://en.wikipedia.org/wiki/Zero-width_space) character:

In LaTeX: \hspace{0pt}  
In TeX: \hskip0pt

Both methods work in Pandoc.

This URL will be too long:  
https://twitter.com/florian_cramer/status/474683019002130433

This one will allow line break:

[https://twitter.com/\hspace{0pt}florian_cramer/status/474683019002130433](https://twitter.com/florian_cramer/status/474683019002130433)