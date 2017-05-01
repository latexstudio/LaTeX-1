# ABOUT
 
This package provides the LaTeX2e class *classycv* for writing job applications.

## FEATURES

* various easy-to-use **commands for drawing components** (such as headings with icons, small charts and progress bars)
* provision of **default components** (for cover letter and resume and their nested components)
* high level of **customization** (through command and enviroment options as well as custom component defintions)
* support for **standardized letter formats** for cover letter (such as DIN-5008 compliant letters)

# USAGE

## GETTING STARTED

Simply copy the file 

> classycv.cls

into the same folder as your cv folder. 

Another option is to add `classycv.cls` as a local class file. The correct way of adding a local class file depends on your platform and LaTeX distribution. A thorough instruction for multiple platforms/distributions can be found on [Stack Overflow](http://tex.stackexchange.com/questions/1137/where-do-i-place-my-own-sty-or-cls-files-to-make-them-available-to-all-my-te).

## CREATING A BASIC CV

In your `<cv-file>.tex` file set the document class to `classycv` using the `\documentclass` command (the options `a4paper, 12pt` for default paper size and default font size are recommended but not required). A simple document created with this class contains

1. a **cover letter** (using the `CoverLetter` environment)
2. a **resume** (using the `Resume` environment)
3. **attachments** (using the `attachment` command)

A template for a basic cv document looks like this:

```
\documentclass[a4paper, 12pt]{classycv}

\begin{document}

%! Cover letter.
\begin{CoverLetter}[<options?>]{<submitter-information>}{<recipient-information>}{<subject-line>}{<opening-line>}{<closing-line>}
<body-text>
\end{CoverLetter}

%! Resume
\begin{Resume}[<options>]{<data>}%
<resume-text>
\end{Resume}

%! Attachments
\attachment[<options>][<name>][<pdf-options>]{<file-1>}
...
\attachment[<options>][<name>][<pdf-options>]{<file-N>}
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

Depending on environment additional commands become available locally through the use of aliases. These are listed in subsections for the respective command or environment.

### THE `CoverLetter` ENVIRONMENT

Basic syntax for this environment is

```
\begin{CoverLetter}[<options>]{<submitter-information>}{<recipient-information>}{<subject-line>}{<opening-line>}{<closing-line>}
<body-text>
\end{CoverLetter}
```

where `<name>` signifies a code or text place holder.

#### Option keys and meaning

Options keys and their meaning depend on the cover letter format and are shown in the respective section.

#### Mandatory arguments

##### First argument (submitter information)

Provides a *pgfkeys* key-val interface (entries of format `<key>=<value>` delimited by commas) to setting submitter information. Example submitter information entries  are `title`, `name` and the address values (`street`, `house`, `zipcode`, `city`, `country`).

Available keys:

* `title`: submitter title (such as "Dr.")
* `name`: submitter full name (first and last name)
* `organisation`: submitter organisation name (such as "Apple Inc.")
* `position`: submitter job position (such as "CEO")
* `street`: submitter street name
* `house`: submitter house number
* `zipcode`: submitter postal zipcode
* `city`: submitter city name
* `country`: submitter country of residence
* `phone`: submitter landline phone number
* `mobile`: submitter mobile phone number
* `fax`: submitter fax number
* `email`: submitter email address
* `website`: submitter website address
* `date`: submission date
* `attachments`: attachment file names or description

> **Note:** Unless otherwise indicated all values are initially and by default set to `\@empty`. If no value is provided the corresponding lines or components are omitted.

##### Second argument (recipient information)

Provides a *pgfkeys* key-val interface (entries of format `<key>=<value>` delimited by commas) to setting recipient information. Example recipient information entries are `title`, `name` and the address values (`street`, `house`, `zipcode`, `city`, `country`).

Available keys:

* `title`: recipient title (such as "Dr.")
* `name`: recipient full name (first and last name)
* `organisation`: recipient organisation name (such as "Apple Inc.")
* `position`: recipient job position (such as "CEO")
* `street`: recipient street name 
* `house`: recipient house number
* `zipcode`: recipient postal zipcode
* `city`: recipient city name 
* `counter`: recipient country name

> **Note:** Unless otherwise indicated all values are initially and by default set to `\@empty`. If no value is provided the corresponding lines or components are omitted.

##### Third argument (subject line)

The letter subject such as 

> "Application — Senior Software Developer (m/f)"

##### Fourth argument (opening line)

The letter opening line such as 

> "To who it may concern,"

##### Fifth argument (closing line)

The letter closing line such as 

> "Kind regards,"

### COVER LETTER FORMATS

#### DIN 5008 A

...

### THE `Resume` ENVIRONMENT

#### Option keys and meanings

...

#### Mandatory arguments

...

#### Local commands and environments

The commands 

* `\heading` (draws a simple heading with optional label)
* `\bar` (draws a simple horizontal line)
* `\progress` (draws a progress bar)
* `\semicircle` (draws a semicircle with optional label)	
* `\doughnut` (draws a doughnut chart with labels)

and the environment `Table` (a wrapper for the environment `tabular` with additional options).


#### RESUME FORMATS

##### Thirty Seventy Resume Format

...

### THE `\attachment` COMMAND

...
