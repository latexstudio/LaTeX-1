# ABOUT
 
This package provides the LaTeX2e class *classycv* for writing job application documents.

## FEATURES

* standard letter formats for cover letters (such as DIN-5008 compliant)
* various commands for layout components such as headings and drawings
* high level of customization through command and enviroment options as well as custom component defintions

# USAGE

## GETTING STARTED

Simply copy the file 

> classycv.cls

into the same folder as your cv folder. 

Another option is to add `classycv.cls` as a local class file. The correct way of adding a local class file depends on your platform and LaTeX distribution. A thorough instruction for multiple platforms/distributions can be found on [Stack Overflow](http://tex.stackexchange.com/questions/1137/where-do-i-place-my-own-sty-or-cls-files-to-make-them-available-to-all-my-te).

## CREATING A BASIC CV

In your `<cv-file>.tex` file set the document class to `classycv` using the `\documentclass` command (the options `a4paper, 12pt` for default paper size and default font size are recommended but not required). A simple document created with this class contains

1. a cover letter (using the `CoverLetter` environment)
2. a resume (using the `Resume` environment)
3. attachments (using the `attachment` command)

For example:

```
\documentclass[a4paper, 12pt]{classycv}

\begin{document}

%! Cover letter.
\begin{CoverLetter}[<options?>]{%
	<submitter-information>
}{%
	<recipient-information>
}{%
	<subject-line>
}{%
	<opening-line>
}{%
	<closing-line>
}
\end{CoverLetter}

%! Resume
\begin{Resume}[<options?>]{%
}{%
}%
<resume-text>
\end{Resume}

%! Attachments
\attachment{<file-1>}
...
\attachment{<file-N>}
\end{document}
```

## PUBLIC INTERFACE

*classycv* exposes the global commands

* `\classycvSet` (set the value of the data entry associated with the given key)
* `\classycvGet` (get the value of the data entry associated with the given key)
* `\classycvClear` (clear the value of the data entry associated with the given key)
* `\classycvDefineComponent` (define a component identified by the given path)
* `\attachment`

and the environments

* `CoverLetter`
* `Resume`

Depending on environment additional commands become available locally. These are listed in the following subsections

### Local commands and environment within `Resume`

The commands 

* `\heading` (draws a simple heading with optional label)
* `\bar` (draws a simple horizontal line)
* `\progress` (draws a progress bar)
* `\semicircle` (draws a semicircle with optional label)	
* `\doughnut` (draws a doughnut chart with labels)

and the environment `Table` (a wrapper for the environment `tabular` with additional options).
