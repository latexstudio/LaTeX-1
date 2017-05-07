%
%! A LaTeX2e class for writing applications. 
%
\NeedsTeXFormat{LaTeX2e}
\ProvidesClass{classycv}[2016/12/21 A LaTeX2e class for writing applications.]

%
% !ref http://stackoverflow.com/a/587054
%
\DeclareOption*{\PassOptionsToClass{\CurrentOption}{article}}
\ProcessOptions
\LoadClass{article}

%!%!%!%!%!%!%!%!
% dependencies %
%!%!%!%!%!%!%!%!
%
%!note For `\DeclareUnicodeCharacter`
%
\RequirePackage[utf8]{inputenc}
\RequirePackage{pgfkeys}
\RequirePackage[%
	%! This parameter has to be declared in order for `\loadgeometry` to change the layout.
	pass%
	, margin=0pt%
]{geometry}
\RequirePackage{titleps}
\RequirePackage{tikz}
\RequirePackage{pdftexcmds}
\RequirePackage{environ}
%!note for maximum width nodes
%!ref http://tex.stackexchange.com/a/46479
\RequirePackage{varwidth}
%!note Minipage like environment with customizable left and right margins
%!ref http://tex.stackexchange.com/a/32707
\RequirePackage{changepage}
%!note For `\getpagerefnumber` (extract number values from page labels).
\RequirePackage{refcount}
%!note For `\adjustbox` and `\marginbox`
%!ref http://tex.stackexchange.com/a/28638
\RequirePackage{adjustbox}
\RequirePackage{tabularx}
\RequirePackage{color}
%!note For cover letter icons.
\RequirePackage{marvosym}
%!note For `\href`.
\RequirePackage[hidelinks]{hyperref}
%!note For `\colorlet`.
\RequirePackage{xcolor}
%!note For `\includegraphics`.
\RequirePackage{graphicx}
%!note For `\tcbox`.
\RequirePackage{tcolorbox}
%!note For symbols.
\RequirePackage{textcomp}
%!note For `H` parameter in figure environments.
\RequirePackage{float}
%!note For symbols.
\RequirePackage{fontawesome}
%!note For `\DeclareDocumentCommand`.
\RequirePackage{xparse}
%!note For `\StrSplit`
\RequirePackage{xstring}
%!note For `\includepdf`
\RequirePackage{pdfpages}
%!note For Lato font.
\RequirePackage{lato}
%!note For Roboto font.
\RequirePackage{roboto}
%!note For Computer Modern Bright font.
\RequirePackage{cmbright}
%!note For Latin Modern font.
\RequirePackage{lmodern}
%!note For Bytestream Vera font.
\RequirePackage{bera}
%!note For `\larger` and `\smaller`.
\RequirePackage{relsize}
%!note For `\LetLtxMacro`
%!href http://tex.stackexchange.com/a/116705
\RequirePackage{letltxmacro}
%!note For boolean macros and `\ifthenelse`.
\RequirePackage{ifthen}

%!%!%!%!%!%!%
% variables %
%!%!%!%!%!%!%

%!old \newsavebox{\classycv@Resume@PutEntry@savebox}

\providecommand{\classycv@arguments}{}


%
%! General purpose length register.
%
\newlength{\classycv@variables@lengthI}
\setlength{\classycv@variables@lengthI}{0pt}

\newlength{\classycv@variables@lengthII}
\setlength{\classycv@variables@lengthII}{0pt}

%
%! General purpose counter registers.
%
\newcounter{classycv@variables@counterI}
\setcounter{classycv@variables@counterI}{0}

\newcounter{classycv@variables@counterII}
\setcounter{classycv@variables@counterII}{0}

%! Default `\parindent` length
\newlength{\classycv@parindent@default}
\setlength{\classycv@parindent@default}{\parindent}

%! Default `\parskip` length
\newlength{\classycv@parskip@default}
\setlength{\classycv@parskip@default}{\parskip}

%! Default `\baselineskip` length
\newlength{\classycv@baselineskip@default}
\setlength{\classycv@baselineskip@default}{\baselineskip}

%! Default `\tabcolsep` length
\newlength{\classycv@tabcolsep@default}
\setlength{\classycv@tabcolsep@default}{\tabcolsep}

%! Cover letter counter
\newcounter{classycv@coverLetterCounter}
\setcounter{classycv@coverLetterCounter}{0}

\newcounter{classycv@coverLetterPageCounter}

\newcounter{classycv@attachmentCounter}
\setcounter{classycv@attachmentCounter}{0}

%! General purpose boolean

\newboolean{classycv@boolean}
\setboolean{classycv@boolean}{false}%

%! Cover letter environment flag
\newif\ifcoverletter
	\coverletterfalse
	
%! Reume environment flag
\newif\ifresume
	\resumefalse

%!%!%!%!%!%!
% commands %
%!%!%!%!%!%!

\makeatletter

% % % % %
% basic %
% % % % %

%
%! font selection
%
\newcommand{\cmrfamily}{\fontfamily{cmr}\selectfont}
\newcommand{\lmrfamily}{\fontfamily{lmr}\selectfont}
\newcommand{\cmbrfamily}{\fontfamily{cmbr}\selectfont}
\renewcommand{\robotofamily}{\fontfamily{Roboto-LF}\selectfont}
\newcommand{\berafamily}{\fontfamily{fve}\selectfont}

%
%! strings
%

%! Intersperse all characters within the second given string with the first given string.
\newcommand{\classycv@intersperse}[2]{%
	%! This should not be reached.
	\ifnum\pdf@strcmp{#2}{\@empty}=\z@%
	\else%
		%! Split at the first character.
		\StrSplit{#2}{1}{\classycv@a}{\classycv@b}%
		%! Last character?
		\ifnum\pdf@strcmp{\classycv@b}{\@empty}=\z@%
			%! Yes: put last character.
			\classycv@a%
		\else%
			%! No: intersperse and continue.
			\classycv@a#1\classycv@intersperse{#1}{\classycv@b}%
		\fi%
	\fi%
}

%
%! decoration
%
\newcommand{\classycv@wrapWithCircle}[2][]{%
%! Were optional arguments given?
\ifnum\pdf@strcmp{#1}{\@empty}=\z@%
	%! No: don't pass to node.
	\tikz[baseline=(char.base)]{\node[inner sep=1pt, draw, circle, thick] (char) {#2};}
\else%
	%! Yes: pass to node.
	\tikz[baseline=(char.base)]{\node[inner sep=1pt, draw, circle, draw, thick, #1] (char) {#2};}
\fi}

\newcommand*\circled[1]{\tikz[baseline=(char.base)]{
            \node[shape=circle,draw,inner sep=2pt] (char) {#1};}}

\newcommand{\classycv@wrapWithHexagon}[2][]{%
%! Were optional arguments given?
\ifnum\pdf@strcmp{#1}{\@empty}=\z@%
	%! No: don't pass to node.
	\tikz[baseline=(text.base)]{\node[inner sep=1pt, regular polygon, regular polygon sides=6, draw, thick, color=light-gray] (text) {#2};}
\else%
	%! Yes: pass to node.
	\tikz[baseline=(text.base)]{\node[inner sep=1pt, regular polygon, regular polygon sides=6, draw, thick, color=light-gray, #1] (text) {#2};}
\fi}

%
% Test if the parameter expands to a zero width box 
%!ref http://tex.stackexchange.com/a/42284
%!old?
\newcommand{\classycv@producesEmpty}[1]{%
  \sbox0{#1}%
  \ifdim\wd0=0pt%
    \numexpr1%
  \else%
  	\numexpr0%
  \fi%
}

%! Single page attachment.
\DeclareDocumentCommand{\attachment}{O{} O{} O{} m}{%
	\bgroup%
	%! Increase counter; label first page.
	\stepcounter{classycv@attachmentCounter}%
	\label{attachment-\theclassycv@attachmentCounter-first-page}%
	%! set data.
	\ifnum\pdf@strcmp{\@empty}{#1}=\z@\else\pgfkeys{/classycv/data/attachment/.cd, #1}\fi%
	\ifnum\pdf@strcmp{\@empty}{#2}=\z@\else\pgfkeys{/classycv/data/attachment/options/.cd, #2}\fi%
	%! Set default components.
	\@ifundefined{/classycv/components/attachment/footer}{\classycvDefineComponent{/attachment/footer}{\classycv@attachment@footerComponent}}{}%
	%! Set format.
	\pagestyle{attachment}%
	\loadgeometry{attachment}%
	\clearpage
	%! Put included pdf.
	\ifnum\pdf@strcmp{#3}{\@empty}=\z@% test if PDF options were passed
		\includepdf[pages={1-}, height=\paperheight-10mm, keepaspectratio, pagecommand={\pagestyle{attachment}}]{#4}%
	\else%
		\includepdf[pages={1-}, height=\paperheight-10mm, keepaspectratio, pagecommand={\pagestyle{attachment}}, #3]{#4}%
	\fi%
	%! Label last page.
	\label{attachment-\theclassycv@attachmentCounter-last-page}%
	\egroup%
}

% % % % % %
% colors  %
% % % % % %

\definecolor{nearly-black}{RGB}{10, 10, 10}
\definecolor{nearly-white}{RGB}{245, 245, 245}
\definecolor{light-gray}{RGB}{200, 200, 200}
\definecolor{medium-gray}{RGB}{127, 127, 127}
\definecolor{dark-gray}{RGB}{55, 55, 55}
%\definecolor{accent-background}{RGB}{24, 42, 64}%! almost navy blue
\definecolor{accent-background}{RGB}{48, 84, 128}
%\definecolor{accent-foreground}{RGB}{24, 242, 196}
\colorlet{accent-foreground}{nearly-white}

% % % % % % %
% classycv  %
% % % % % % %

%
%! constants
%
\newcommand{\classycv@FORMAT@COVERLETTER@DINLETTERA}{din-5008-a}
\newcommand{\classycv@FORMAT@COVERLETTER@DINLETTERB}{din-5008-b}
\newcommand{\classycv@FORMAT@RESUME@TWENTYEIGHTY}{twenty-eighty}
\newcommand{\classycv@FORMAT@RESUME@THIRTYSEVENTY}{thirty-seventy}
\newcommand{\classycv@FORMAT@RESUME@FOURTYSIXTY}{fourty-sixty}

%
% Set, get and clear cv data
%
\providecommand{\classycvSet}[2]{\pgfkeyssetvalue{/classycv/data#1}{#2}}
\providecommand{\classycvGet}[2]{\pgfkeysvalueof{/classycv/data#1}}
\providecommand{\classycvClear}[2]{\pgfkeyssetvalue{/classycv/data#1}{\@empty}}

%
% Define a component.
%
\providecommand{\classycvDefineComponent}[2]{%
	\@namedef{/classycv/components#1}{#2}%
}

%
%! Put CV data.
%
\providecommand{\classycv@PutComponent}[1]{%
	\bgroup%
	%! put component
	\@ifundefined{/classycv/components#1}{%
		\ClassWarning{classycv}{missing component ``#1''}%
	}{%
		\csname/classycv/components#1\endcsname%
	}%
	\egroup%
}

%
%! Put a simple horizontal bar.
%! #1: options
%! #2: bar color
%
\providecommand{\classycv@PutBar}[2][]{%
	\bgroup%
	\pgfkeys{/classycv/data/put bar/options/.cd, #1}
	\pgfkeys{%
		/classycv/data/put bar/options/.cd%
		, width/.get=\width%
		, height/.get=\height%
		, strength/.get=\strength%
		, skip above/.get=\skipAbove%
		, skip below/.get=\skipBelow%
	}%	
	\vspace*{\skipAbove}\par%
	\tikz{
		\draw[use as bounding box, draw=none, inner sep=0pt] rectangle (\width, \height);%
		\path[draw, line width=\strength, color=#2] (current bounding box.west) -- (current bounding box.east);%
	}%
	\vspace*{\skipBelow}\par%
	\egroup%
}

%
%! Put a simple horizontal progress bar.
%! #1: options
%! #2: completion percentage
%
\providecommand{\classycv@PutProgressBar}[2][]{%
	\bgroup%
	\pgfkeys{/classycv/data/put progress bar/options/.cd, #1}%
	\pgfkeys{%
		/classycv/data/put progress bar/options/.cd%
		, height/.get=\height%
		, background color/.get=\backgroundColor%
		, foreground color/.get=\foregroundColor%
%		, has border/.get=\hasBorder%
		, border width/.get=\borderWidth%
		, border color/.get=\borderColor%
		, bar width/.get=\barWidth%
		, has label/.get=\hasLabel%
		, label width/.get=\labelWidth%
		, label position/.get=\labelPosition%
		, label font/.get=\labelFont%
		, label color/.get=\labelColor%
		, label text/.get=\labelText%		
		, label text align/.get=\labelTextAlign%
		, skip between/.get=\skipBetween%
	}%
%\typeout{(!) classycv@PutProgressBar}%
	\setlength{\classycv@variables@lengthI}{\barWidth}%
	\divide\classycv@variables@lengthI by 100\relax%
	\multiply\classycv@variables@lengthI by #2\relax%
%\show\classycv@variables@lengthI
	\begin{tikzpicture}%
		\ifnum\pdf@strcmp{yes}{\hasLabel}=\z@%
			\ifnum\pdf@strcmp{left}{\labelPosition}=\z@%
				\begin{pgfonlayer}{background}%
					\node[%
						anchor=north west%
						, minimum width=\labelWidth%
						, minimum height=\height%
						, text width=\labelWidth%
						, inner sep=0pt%
						, outer sep=0pt%
						, font=\labelFont%
						, text=\labelColor%
						, align=\labelTextAlign] (label) {\labelText};%
					\coordinate (P1) at ($([shift={(\skipBetween, 0)}]label.south east)$);%
					\draw[text width=, line width=\borderWidth, draw=\borderColor, fill=\backgroundColor] (P1) rectangle +(\barWidth, \height);%
				\end{pgfonlayer}%
				\begin{pgfonlayer}{main}%
					\coordinate (P2) at ($([shift={(\skipBetween + \borderWidth, \borderWidth)}]label.south east)$);%
					\draw[draw=none, fill=\foregroundColor] (P2) rectangle +(\classycv@variables@lengthI, \height);%
				\end{pgfonlayer}%
			\else%
				\begin{pgfonlayer}{background}%
					\draw[text width=, line width=\borderWidth, draw=\borderColor, fill=\backgroundColor] (0, 0) rectangle +(\barWidth, \height);%
					\coordinate (P1) at (\barWidth, 0);%
					\coordinate (P2) at ($([shift={(\skipBetween, 0)}]P1.south east)$);%
					\node[%
						above right=0pt and 0pt of P2%
						, minimum width=\labelWidth%
						, minimum height=\height%
						, text width=\labelWidth%
						, inner sep=0pt%
						, outer sep=0pt%
						, font=\labelFont%
						, text=\labelColor%
						, align=\labelTextAlign] (label) {\labelText};%
				\end{pgfonlayer}%
				\begin{pgfonlayer}{main}%
					\draw[draw=none, fill=\foregroundColor] (\borderWidth, \borderWidth) rectangle +(\classycv@variables@lengthI, \height);%
				\end{pgfonlayer}%
			\fi%
		\else%
		\fi%
	\end{tikzpicture}%
	\egroup%
}
%
%! Put a semi circle
%! #1: completion percentage x (x = 0,...,100)
%!href: http://tex.stackexchange.com/a/15983
%
\providecommand{\classycv@PutSemicircle}[2][]{%
	\bgroup%
	\pgfkeys{/classycv/data/put semicircle/options/.cd, #1}%
	\pgfkeys{%
		/classycv/data/put semicircle/options/.cd%
		, size/.get=\size%
		, strength/.get=\strength%
		, line color/.get=\lineColor%
		, fill color/.get=\fillColor%
		, has label/.get=\hasLabel%
		, label text/.get=\labelText%
		, label font/.get=\labelFont%
		, label color/.get=\labelColor%
		, draw complement/.get=\drawComplement%
		, complement line color/.get=\complementLineColor%
		, draw glow/.get=\drawGlow%
	}%
	\tikz{%	
		\pgfmathsetmacro\arcLength{(#2/100)*360}%
		\pgfmathsetmacro\endDegree{Mod(\arcLength, 360)}%
		%! Normalize to 360 degrees if `\arcLength` is any multiple of 360 greater than 0.
		\ifnum0 = \endDegree\relax%
			\ifnum0 < #2\relax%
				\pgfmathsetmacro\endDegree{360}%
			\fi%
		\fi%
		\setlength{\classycv@variables@lengthI}{\dimexpr0.5\size\relax}%
%		\draw[black, use as bounding box] rectangle (\size, \size);%
		\begin{pgfonlayer}{main}
		    \draw[use as bounding box, draw=\lineColor, fill=\fillColor, rotate=270, line width=\strength] (0, 0) arc (0:\endDegree:\size);%
		\end{pgfonlayer}{main}
		%! Draw a glow effect?
		\ifnum\pdf@strcmp{yes}{\drawGlow}=\z@%
			\begin{pgfonlayer}{background}
			    \draw[draw=none, fill=none, circular glow={fill=light-gray!50!nearly-white}, rotate=270] (0, 0) arc (0:360:\size);%
			\end{pgfonlayer}%
		\fi%
		%! Draw complement?
		\ifnum\pdf@strcmp{yes}{\drawComplement}=\z@%
			\begin{pgfonlayer}{overlay 1}
				\draw[draw=\complementLineColor, fill=\fillColor, line width=\strength, rotate=270] (0, 0) arc (360:\endDegree:\size);			
		    \end{pgfonlayer}%
		\fi%
		%! Draw label?
		\ifnum\pdf@strcmp{yes}{\hasLabel}=\z@%
			\begin{pgfonlayer}{overlay 2}%
			    \node[draw=none, minimum size=\size, text width=, text=\labelColor, font=\labelFont] at (current bounding box.center) {\labelText};%
			\end{pgfonlayer}
		\fi%
	}%
	\egroup%
}

%
%! Put a doughnut chart.
%! #1: options
%! #2: completion percentage
%!ref https://tex.stackexchange.com/a/66219
%!usage \classycv@PutDoughnutChart[<options>]<sectors>; where <elements> is a CSV list of pairs `(<name>, <percentage>)` containing the sectors of the doughnut. Each sector is defined by a name and a percentage value.
\providecommand{\classycv@PutDoughnutChart}[2][]{%
	\pgfkeys{/classycv/data/put doughnut chart/options/.cd, #1}%
	\pgfkeys{%
		/classycv/data/put doughnut chart/options/.cd%
		, size/.get=\size%
		, strength/.get=\strength%
		, line color/.get=\lineColor%
		, label size/.get=\labelSize%
		, label shape/.get=\labelShape%
		, label line color/.get=\labelLineColor%
		, label fill color/.get=\labelFillColor%
		, label text color/.get=\labelTextColor%
		, basic style/.get=\basicStyle%
	}%
	\setcounter{classycv@variables@counterI}{0}% arc start
	\setcounter{classycv@variables@counterII}{0}% arc end
	\begin{tikzpicture}[%
		extended line/.style={shorten >=-##1,shorten <=-##1}
		, extended line/.default=1cm
		, right extended line/.style={shorten >=-##1}
		, right extended line/.default=1cm
	]%
		\draw[draw=none, use as bounding box, inner sep=0pt, outer sep=0pt] rectangle (\size, \size);
		\foreach \x [count=\i] in {#2} {%
			\StrCut{\x}{/}\label\r%
			\StrCut{\r}{/}\percentage\lineColor%
			\setcounter{classycv@variables@counterI}{0}%
			\addtocounter{classycv@variables@counterI}{\theclassycv@variables@counterII}%
			\setcounter{classycv@variables@counterII}{\numexpr 360 *\percentage/100\relax}%
			\setcounter{classycv@variables@counterII}{\numexpr\theclassycv@variables@counterI + \theclassycv@variables@counterII}%
			\draw[\lineColor, line width=\strength] ([shift=(\theclassycv@variables@counterI:\dimexpr0.5\dimexpr\size-\strength\relax)]\dimexpr0.5\size\relax,\dimexpr0.5\size\relax) arc (\theclassycv@variables@counterI:\theclassycv@variables@counterII:\dimexpr0.5\dimexpr\dimexpr\size-\strength\relax) coordinate[below, midway] (P\i); 
			\node[below right=-0.5em and -0.5em of P\i, text width=\labelSize, align=center, inner sep=0pt, outer sep=0pt, \labelShape, draw=\labelLineColor, fill=\labelFillColor, text=\labelTextColor] {\basicStyle\label};
	};%
	\end{tikzpicture}%
}

%
%! Put a heading.
%
\providecommand{\classycv@PutHeading}[2][]{%
	\bgroup%
	\pgfkeys{/classycv/data/put heading/options/.cd, #1}%
	\pgfkeys{%
		/classycv/data/put heading/options/.cd%
		, width/.get=\width%
		, height/.get=\height%
		, has label/.get=\hasLabel%
		, label shape/.get=\labelShape%
		, label color/.get=\labelColor%
		, label frame color/.get=\labelFrameColor%
		, label frame width/.get=\labelFrameWidth%
		, label inner sep/.get=\labelInnerSep%
		, label position/.get=\labelPosition%
		, label text/.get=\labelContent%
		, label text color/.get=\labelTextColor%
		, basic style/.get=\basicStyle%
		, skip above/.get=\skipAbove%
		, skip below/.get=\skipBelow%
		, skip between/.get=\skipBetween%
	}%
	\vspace*{\skipAbove}\par%
	\basicStyle%
	\setlength{\classycv@variables@lengthI}{\dimexpr\labelInnerSep+\labelFrameWidth\relax}%
	\tikz[baseline=(label.base)]{%
		\draw[use as bounding box, draw=none] rectangle (\width, \height);%
		%! Is a label required?
		\ifnum\pdf@strcmp{yes}{\hasLabel}=\z@%
			%! Is the label left or right?
			\ifnum\pdf@strcmp{left}{\labelPosition}=\z@%
				\node[right=\classycv@variables@lengthI of current bounding box.west, inner sep=\labelInnerSep, text width=, \labelShape, line width=\labelFrameWidth, draw=\labelFrameColor, fill=\labelColor, align=center, font={\smaller[2]}, text=\labelTextColor] (label) {\labelContent};%
				\node[
					right=\skipBetween of label.east%
					, text width=%
				] (text) {#2};%
			\else%
				\node[right=0pt of current bounding box.west, text width=] (text) {#2};%
				\node[right=\skipBetween of text.east, inner sep=\labelInnerSep, text width=, \labelShape, line width=\labelFrameWidth, draw=\labelFrameColor, fill=\labelColor, align=center, font={\smaller[2]}, text=\labelTextColor] (label) {\labelContent};%
			\fi%
		\else%
			\node[below right=0pt and 0pt of current bounding box.north west] (text) {#2};%
		\fi%
	}%
	\vspace*{\skipBelow}\par%
	\egroup%
}

\newenvironment{classycv@PutTable}[1][]{%
	\bgroup%
	\pgfkeys{/classycv/data/put table/options/.cd, #1}%
	\pgfkeys{%
		/classycv/data/put table/options/.cd%
		, width/.get=\width%
		, basic style/.get=\basicStyle%
		, column format/.get=\columnFormat%
		, stretch/.get=\stretch%
%		, alignment/.get=\alignment$
		, skip above/.get=\skipAbove%
		, skip below/.get=\skipBelow%
	}%
	\vspace*{\skipAbove}\par%
	\basicStyle%
	\renewcommand{\arraystretch}{\stretch}%
	%! begin tabular
	\expandafter\tabular\expandafter{\columnFormat}%
}{%
	%! end tabular
	\endtabular%
	\vspace*{\skipBelow}\par%
	\egroup%
}

%
% Cover letter environment.
%!todo optional parameter
%
\newenvironment{CoverLetter}[6][]{%
	%! Check if this was called within a cover letter environment
	\ifcoverletter\errmessage{Terminal error: detected invalid nested cover letter environment}\else\fi%
	\coverlettertrue%
	%! Increase the cover letter counter
	\stepcounter{classycv@coverLetterCounter}%
	%! Reset the cover letter page counter
	\setcounter{classycv@coverLetterPageCounter}{0}%
	%! Label the first page
	\label{cover-letter-\theclassycv@coverLetterCounter-first-page}%
	%! switch for the letter format
	\pgfkeys{/classycv/data/settings/cover letter/format/.get=\classycv@format}%
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@COVERLETTER@DINLETTERA}=\z@%
		%! DIN 5008 A format
		\begin{classycv@PutCoverLetterDINLetterA}[#1]{#2}{#3}{#4}{#5}{#6}%
	\else%
		%!...
		%! invalid letter format
		\ClassWarning{classycv}{! undefined letter format (\classycv@format)}%
	\fi%
}{%
	%! switch for the letter format
	\pgfkeys{/classycv/data/settings/cover letter/format/.get=\classycv@format}%
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@COVERLETTER@DINLETTERA}=\z@%
		%! DIN 5008 A format
		\end{classycv@PutCoverLetterDINLetterA}%
	\fi%
	%! Label the last page
	\label{cover-letter-\theclassycv@coverLetterCounter-last-page}%
	%! Reset cover letter flag
	\coverletterfalse%
}


%
%! A DIN 5008 type A conformant cover letter
%
\newenvironment{classycv@PutCoverLetterDINLetterA}[6][]{%
	\bgroup%
	%! Set data
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/.cd, #1}
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/submitter/.cd, #2}
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/recipient/.cd, #3}
	\pgfkeys{%
		/classycv/data/cover letter/DIN 5008 A/.cd%
		, subject={#4}%
		, opening={#5}%
		, closing={#6}%
	}%
	%! Set default components
	\@ifundefined{/classycv/components/cover letter/header}{\classycvDefineComponent{/cover letter/header}{\classycv@PutCoverLetterDINLetterA@headerComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/footer}{\classycvDefineComponent{/cover letter/footer}{\classycv@PutCoverLetterDINLetterA@footerComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/recipient information}{\classycvDefineComponent{/cover letter/recipient information}{\classycv@PutCoverLetterDINLetterA@recipientInformationComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/submitter information}{\classycvDefineComponent{/cover letter/submitter information}{\classycv@PutCoverLetterDINLetterA@submitterInformationComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/subject}{\classycvDefineComponent{/cover letter/subject}{\classycv@PutCoverLetterDINLetterA@subjectComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/date}{\classycvDefineComponent{/cover letter/date}{\classycv@PutCoverLetterDINLetterA@dateComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/opening}{\classycvDefineComponent{/cover letter/opening}{\classycv@PutCoverLetterDINLetterA@openingComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/closing}{\classycvDefineComponent{/cover letter/closing}{\classycv@PutCoverLetterDINLetterA@closingComponent}}{}%
	\@ifundefined{/classycv/components/cover letter/attachments}{\classycvDefineComponent{/cover letter/attachments}{\classycv@PutCoverLetterDINLetterA@attachmentsComponent}}{}%
	%! Set geometry and page style
	\loadgeometry{din-5008-a}%
	\pagestyle{cover-letter}%
	%! Recipient address and submitter information boxes	
	\pgfkeys{
		/classycv/data/cover letter/DIN 5008 A/options/.cd%
		, recipient information line color/.get=\recipientInformationLineColor%
		, recipient information padding/.get=\recipientInformationPadding%		
		, submitter information line color/.get=\submitterInformationLineColor%
		, submitter information padding/.get=\submitterInformationPadding%
	}%
	\begin{adjustbox}{margin=20mm 8.46mm 10mm 0mm, minipage=[t][45mm][t]{180mm}}%
		\begin{tikzpicture}
			\draw[use as bounding box, draw=none] (0, 0) rectangle (180mm, 55mm);%
			\node[below right=0pt and 0pt of current bounding box.north west, inner sep=\recipientInformationPadding, draw=\recipientInformationLineColor] {%
				\begin{adjustbox}{minipage=[t][45mm-\dimexpr2\dimexpr\recipientInformationPadding\relax][c]{85mm-\dimexpr2\dimexpr\recipientInformationPadding\relax}}%
					\classycv@PutComponent{/cover letter/recipient information}%
				\end{adjustbox}%		
			};%	
			\node[below left=5mm and 0pt of current bounding box.north east, inner sep=\submitterInformationPadding, draw=\submitterInformationLineColor] {%
%				\let\@minipagerestore=\raggedright%
				\begin{adjustbox}{minipage=[t][50mm-\dimexpr2\dimexpr\submitterInformationPadding\relax][c]{75mm-\dimexpr2\dimexpr\submitterInformationPadding\relax}}%
					\classycv@PutComponent{/cover letter/submitter information}%
				\end{adjustbox}%		
			};%
		\end{tikzpicture}%
	\end{adjustbox}\newline%
	%! Optional letter body separator.
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/has body separator/.get=\hasBodySeparator}%
	\ifnum\pdf@strcmp{yes}{\hasBodySeparator}=\z@%
		\tikz{%
			\draw[draw=none, use as bounding box] rectangle (\linewidth, \baselineskip);
			\coordinate (P1) at ($([shift={(25mm, 0)}]current bounding box.north west)$);%
			\coordinate (P2) at ($([shift={(-20mm, 0)}]current bounding box.north east)$);%
			\draw[accent-background] (P1) -- (P2);%
		}\par%
	\else%
		\vspace*{\classycv@baselineskip@default}\par
	\fi%
	%! Text area.
	%!note Margins are implemented using the `adjustwidth` environment with the margins specified in DIN 5008 A. 
	%!note width is A4 paper width (210mm) minus the left and right margins (25mm and 20mm) of the DIN 5008 A letter's text area
	%!ref http://tex.stackexchange.com/a/32707
	\begin{adjustwidth}{25mm}{20mm}%
		%! DIN 5008 A defines unindented lines and one blank line as paragraph separator
		\setlength{\parindent}{0pt}%
		\setlength{\parskip}{\classycv@baselineskip@default}%
		%! Put date component
		\classycv@PutComponent{/cover letter/date}%
		%! Put subject component
		\classycv@PutComponent{/cover letter/subject}%
		%! Put opening component
		\classycv@PutComponent{/cover letter/opening}%
		%! Put content
		\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/content style/.get=\contentStyle}
		\bgroup%
			\contentStyle%
}{%
		\egroup%
		%! Put closing component
		\classycv@PutComponent{/cover letter/closing}%
	\end{adjustwidth}%
	\vspace*{\fill}%
	\clearpage%
	\egroup%
}

%
% Default DIN 5008 A letter components
%

%
%! Default DIN 5008 A letter header component
%
\newcommand{\classycv@PutCoverLetterDINLetterA@headerComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/header repeat/.get=\repeat}%
	%! Determine if the header should be drawn.
	\setboolean{classycv@boolean}{false}%
	\ifnum\pdf@strcmp{yes}{\repeat}=\z@%
		\setboolean{classycv@boolean}{true}%
	\else%
		\ifnum\theclassycv@coverLetterPageCounter=1%
		\setboolean{classycv@boolean}{true}%
		\fi%
	\fi%		
	\ifthenelse{\boolean{classycv@boolean}}{%
		\pgfkeys{%
			/classycv/data/cover letter/DIN 5008 A/options/.cd%
			, header basic style/.get=\basicStyle%
			, header name style/.get=\nameStyle%
			, header address style/.get=\addressStyle%
			, header details style/.get=\detailsStyle%
			, header background color/.get=\bg%
			, header foreground color/.get=\fg%
			, header line color/.get=\lineColor%
		}%
		\pgfkeys{%
			/classycv/data/cover letter/DIN 5008 A/submitter/.cd%
			, title/.get=\title%
			, name/.get=\name%
			, street/.get=\street%
			, house/.get=\house%
			, city/.get=\city%
			, zipcode/.get=\zipcode%
			, phone/.get=\phone%
			, mobile/.get=\mobile%
			, fax/.get=\fax%
			, email/.get=\email%
			, website/.get=\website%
		}%
		\begin{tikzpicture}%
			\draw[draw=\lineColor, use as bounding box, fill=\bg] rectangle (210mm, 27mm);%
			\coordinate (P1) at (20mm, \dimexpr27mm-18pt\relax);%
			\node[below right=0pt and 0pt of P1, inner sep=0pt, outer sep=0pt, text width=170mm, text=\fg] {%
				\basicStyle%
				\setlength{\tabcolsep}{0pt}%
				\begin{tabular*}{\linewidth}{L{0.4\dimexpr\linewidth-2\tabcolsep\relax} L{0.6\dimexpr\linewidth-2\tabcolsep\relax}}%
					\adjustbox{minipage=[c][\dimexpr27mm-36pt\relax][c]{\linewidth}, margin=0pt}{%
						{\nameStyle\name}%
						\\\bgroup%
							\addressStyle%
							%! Put street and house number.
							\ifnum\pdf@strcmp{\street}{\@empty}=\z@\else\ifnum\pdf@strcmp{\house}{\@empty}=\z@\street\else\street~\house\fi\fi%
							%! Put zipcode and city
							\ifnum\pdf@strcmp{\@empty}{\zipcode}=\z@\else%
								%! Put a bullet point as a delimiter if there is preceding text.
								\ifnum\pdf@strcmp{\@empty}{\street}=\z@\else~\textbullet~\fi%
								\ifnum\pdf@strcmp{\@empty}{\city}=\z@\city\else\zipcode~\city\fi%
							\fi%							
						\egroup%
					}%
				&%
					\adjustbox{minipage=[c][\dimexpr27mm-36pt\relax][c]{\linewidth}, margin=0pt}{%
						\detailsStyle%
						\setlength{\tabcolsep}{0pt}%
						\renewcommand{\arraystretch}{1.25}%
						\begin{tabular}[t]{L{0.5\dimexpr\linewidth-2\tabcolsep\relax} L{0.5\dimexpr\linewidth-2\tabcolsep\relax}}%
							\begin{tabular}[t]{C{2.5em} l}
								\ifnum\pdf@strcmp{\phone}{\empty}=\z@\else{\large\Telefon}&\phone\\\fi%
								\ifnum\pdf@strcmp{\mobile}{\empty}=\z@\else{\large\faMobile}&\mobile\fi%
							\end{tabular}% 
							& \begin{tabular}[t]{C{2.5em} l}%
								\ifnum\pdf@strcmp{\email}{\empty}=\z@\else{\large\Letter}&\email\\\fi%
								\ifnum\pdf@strcmp{\website}{\empty}=\z@\else{\large\ComputerMouse}&\website\fi%
							\end{tabular}%
						\end{tabular}%
					}%
				\end{tabular*}%
			};%
			\node[minimum width=15pt, minimum height=7.5pt, below=-4.25pt of current bounding box.south, inner sep=0pt, diamond, draw=\lineColor, fill=\bg] (mark) {};%
		\end{tikzpicture}%
	}{}%
	\egroup%
}

%
%! Default DIN 5008 A letter footer component
%
\newcommand{\classycv@PutCoverLetterDINLetterA@footerComponent}{%
	\bgroup%
	\pgfkeys{%
		/classycv/data/cover letter/DIN 5008 A/options/.cd%
		, has footer separator/.get=\hasFooterSeparator%
		, has page counter/.get=\hasPageCounter%
		, footer style/.get=\style
	}%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/submitter/attachments/.get=\attachments}%
	%! put component
	\begin{tikzpicture}
		\draw[draw=none, use as bounding box] rectangle (\textwidth, 42mm);
		%! Optional footer separator.
		\ifnum\pdf@strcmp{yes}{\hasFooterSeparator}=\z@%
			\coordinate (P1) at ($([shift={(25mm, -4.23mm)}]current bounding box.north west)$);%
			\coordinate (P2) at ($([shift={(-20mm, -4.23mm)}]current bounding box.north east)$);%
			\draw[accent-background] (P1) -- (P2);
		\fi%
		%! Footer content node.
		\node[below right=\dimexpr4.23mm + \baselineskip\relax and 25mm of current bounding box.north west, text width=\dimexpr\textwidth - 45mm\relax, inner sep=0pt, outer sep=0pt] (footer) {%
			\style%
			\ifnum\pdf@strcmp{yes}{\hasPageCounter}=\z@%
				\begin{tabular}[t]{L{0.9\linewidth-2\tabcolsep} R{0.1\linewidth-2\tabcolsep}}%
					%! Put attachments.
						\ifnum\pdf@strcmp{\attachments}{\empty}=\z@\else%
							\setcounter{classycv@variables@counterI}{\the\numexpr\getpagerefnumber{cover-letter-\theclassycv@coverLetterCounter-last-page}-1}%
							\ifnum\thepage=\theclassycv@variables@counterI%
								\faFilesO~~\attachments%
							\fi%
						\fi%
					& %! Put page counter.
						\theclassycv@coverLetterPageCounter~|~\the\numexpr\getpagerefnumber{cover-letter-\theclassycv@coverLetterCounter-last-page}-\getpagerefnumber{cover-letter-\theclassycv@coverLetterCounter-first-page}%
				\end{tabular}%
			\else%
				\ifnum\pdf@strcmp{\attachments}{\empty}=\z@\else%
					\setcounter{classycv@variables@counterI}{\the\numexpr\getpagerefnumber{cover-letter-\theclassycv@coverLetterCounter-last-page}-1}%
					\ifnum\thepage=\theclassycv@variables@counterI%
						\stackbox[l]{\faFilesO~~\attachments}%
					\fi%
				\fi%
			\fi%
		};%
	\end{tikzpicture}
	\egroup%
}

%! Default DIN 5008 A letter recipient information components.
\newcommand{\classycv@PutCoverLetterDINLetterA@recipientInformationComponent}{%
	\bgroup%
	\pgfkeys{%
		/classycv/data/cover letter/DIN 5008 A/options/.cd%
		, recipient information basic style/.get=\basicStyle%
		, recipient information organisation style/.get=\organisationStyle%
		, recipient information name style/.get=\nameStyle%
		, recipient information position style/.get=\positionStyle%
		, recipient information address style/.get=\addressStyle%
	}
	\pgfkeys{%
		/classycv/data/cover letter/DIN 5008 A/submitter/.cd%
		, name/.get=\submitterName%
		, street/.get=\submitterStreet%
		, house/.get=\submitterHouse%
		, zipcode/.get=\submitterZipcode
		, city/.get=\submitterCity
	}%
	\pgfkeys{%
		/classycv/data/cover letter/DIN 5008 A/recipient/.cd%
		, organisation/.get=\organisation%
		, position/.get=\position%
		, title/.get=\title%
		, name/.get=\name%
		, street/.get=\street%
		, house/.get=\house%
		, zipcode/.get=\zipcode%
		, city/.get=\city%
		, country/.get=\country%
	}%
%	\underline{\submitterName~\textbullet~\submitterStreet~\submitterHouse~\textbullet~\submitterZipcode~\submitterCity}%
	\basicStyle
	\vspace*{\classycv@baselineskip@default}%
	\ifnum\pdf@strcmp{\@empty}{\organisation}=\z@\else{\organisationStyle\organisation}\fi%
	\ifnum\pdf@strcmp{\@empty}{\name}=\z@\else\\{\nameStyle\name}\fi%
	\ifnum\pdf@strcmp{\@empty}{\position}=\z@\else\\{\positionStyle\position}\fi%
	\ifnum\pdf@strcmp{\@empty}{\street}=\z@\else\\{\addressStyle\street~\house}\fi%
	\ifnum\pdf@strcmp{\@empty}{\zipcode}=\z@\else\\{\addressStyle\zipcode~\city}\fi%
	\ifnum\pdf@strcmp{\@empty}{\country}=\z@\else\\{\addressStyle\country}\fi%
	\egroup%
}

%
%! Default DIN 5008 A letter submitter information component
%!note Empty by default.
%
\newcommand{\classycv@PutCoverLetterDINLetterA@submitterInformationComponent}{%
}

%! Default DIN 5008 A letter date component
\newcommand{\classycv@PutCoverLetterDINLetterA@dateComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/date/.get=\date}%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/submitter/city/.get=\city}%
	%! Skip the subject line if no subject was specified.
	\ifnum\pdf@strcmp{\@empty}{\date}=\z@%
	\else%
		\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/date line style/.get=\dateStyle}%
		%! Reduce parskip such that the ragged left paragraph appears as a line
		\setlength{\parskip}{0pt}%
		\ifnum\pdf@strcmp{\@empty}{\city}=\z@%
			{\raggedleft\dateStyle\date\par}%
		\else%
			{\raggedleft\dateStyle\city,~\date\par}%
		\fi
		%! DIN 5008 A requires two empty lines after the date line
		\vspace*{\baselineskip}\par%
		\setlength{\parskip}{\classycv@parskip@default}%
	\fi%
	\egroup%
}

%! Default DIN 5008 A letter subject component
\newcommand{\classycv@PutCoverLetterDINLetterA@subjectComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/subject/.get=\subject}%
	%! Skip the subject line if no subject was specified.
	\ifnum\pdf@strcmp{\@empty}{\subject}=\z@%
	\else%
		\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/subject line style/.get=\subjectStyle}%
		{\subjectStyle\subject}%
		%! DIN 5008 A requires two empty lines after the subject line
		\vspace*{2\baselineskip}\par%
	\fi%
	\egroup%
}

%! Default DIN 5008 A letter opening component
\newcommand{\classycv@PutCoverLetterDINLetterA@openingComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/opening/.get=\opening}%
	%! Skip the subject line if no subject was specified.
	\ifnum\pdf@strcmp{\@empty}{\opening}=\z@%
	\else%
		\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/opening line style/.get=\openingStyle}%
		%! Reduce parskip to baseline skip.
		\setlength{\parskip}{0pt}
		%! Append the opening line and add a line skip as per DIN 5008 A requirement.
		{\openingStyle\opening\par}%
	\fi%
	\egroup%
}

%! Default DIN 5008 A letter closing component
\newcommand{\classycv@PutCoverLetterDINLetterA@closingComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/closing/.get=\closing}%
	\pgfkeys{
		/classycv/data/cover letter/DIN 5008 A/submitter/.cd%
		, name/.get=\name%
		, organisation/.get=\organisation%
		, position/.get=\position%
	}%
	%! Insert a line.
	\par%
	\stackbox[l]{%
		%! Skip the closing line if no closing was specified.
		\ifnum\pdf@strcmp{\@empty}{\closing}=\z@%
		\else%
			\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/closing line style/.get=\closingStyle}%
			{\closingStyle\closing}%
		\fi%
		\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/signature basic style/.get=\signatureStyle}%
		\signatureStyle%
		%!note DIN 5008 A requires three empty lines before the rest of the closing block
		\par\addvspace{3\baselineskip}%
		%! Was a submitter name given?
		\ifnum\pdf@strcmp{\@empty}{\name}=\z@%
		\else%
			%! Yes: append to closing block
			\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/signature name line style/.get=\nameStyle}%
			\par{\nameStyle\name}%
		\fi
		%! Was a submitter position given?
		\ifnum\pdf@strcmp{\@empty}{\position}=\z@%
		\else
			%! Yes: append to closing block
			\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/signature position line style/.get=\positionLineStyle}
			\par{\positionLineStyle\position}%
		\fi%
		%! Was a submitter organisation given?
		\ifnum\pdf@strcmp{\@empty}{\organisation}=\z@%
		\else%
			%! Yes: append to closing block
			\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/signature organisation line style/.get=\organisationLineStyle}%
			%!note DIN 5008 A requires one empty line before the organisation line in the closing block
			\par{\organisationLineStyle\organisation}%
		\fi%
	}%
	\egroup%
}

\newcommand{\classycv@PutCoverLetterDINLetterA@attachmentsComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/cover letter/DIN 5008 A/submitter/attachments/.get=\attachments}
	%! Were attachments given?
	\ifnum\pdf@strcmp{\attachments}{\empty}=\z@\else%
		%! Yes: put attachments line.
		\pgfkeys{/classycv/data/cover letter/DIN 5008 A/options/attachments style/.get=\attachmentsStyle}%
		\vfill%
		{\attachmentsStyle\faFilesO~~\attachments}%
	\fi%
	\egroup%
}

%
%!todo more cover letter formats
%

%
% Resume environment.
%
\newenvironment{Resume}[2][]{%
	%! Check if this was called within a resume environment
	\ifresume\errmessage{Terminal error: detected invalid nested resume environment}\else\fi%
	\resumetrue%
	%! aliase component creating commands
	\LetLtxMacro\semicircle\classycv@PutSemicircle%
	\LetLtxMacro\doughnut\classycv@PutDoughnutChart%
%!tmp	\LetLtxMacro\star\classycv@PutStar%
	\LetLtxMacro\progress\classycv@PutProgressBar%
	\LetLtxMacro\heading\classycv@PutHeading%
	\LetLtxMacro\bar\classycv@PutBar%
	\LetLtxMacro{\Table}\classycv@PutTable%
	\LetLtxMacro{\endTable}\endclassycv@PutTable%
	%! switch for the resume format
	\pgfkeys{/classycv/data/settings/resume/format/.get=\classycv@format}%
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@RESUME@FOURTYSIXTY}=\z@%
		%! Fourty Sixty resume format
		\begin{classycv@PutResumeFourtySixty}[#1]{#2}%
	\else%
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@RESUME@THIRTYSEVENTY}=\z@%
		%! Thirty Seventy resume format
		\begin{classycv@PutResumeThirtySeventy}[#1]{#2}%
	\else%
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@RESUME@TWENTYEIGHTY}=\z@%
		%! Twenty Eighty resume format
		\begin{classycv@PutResumeTwentyEighty}[#1]{#2}%
	\else
		%! invalid resume format
		\ClassWarning{classycv}{! undefined letter format (\classycv@format)}%
	\fi\fi\fi%
}{%
	%! switch for the letter format
	\pgfkeys{/classycv/data/settings/resume/format/.get=\classycv@format}%
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@RESUME@FOURTYSIXTY}=\z@%
		%! Fourty Sixty resume format
		\end{classycv@PutResumeFourtySixty}%
	\else
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@RESUME@THIRTYSEVENTY}=\z@%
		%! Thirty Seventy resume format
		\end{classycv@PutResumeThirtySeventy}%
	\else
	\ifnum\pdf@strcmp{\classycv@format}{\classycv@FORMAT@RESUME@TWENTYEIGHTY}=\z@%
		%! Twenty Eighty resume format
		\end{classycv@PutResumeTwentyEighty}%
	\fi\fi\fi%
	%! Reset resume flag
	\resumefalse%
}

%! Fourty Sixty resume format.
\newenvironment{classycv@PutResumeFourtySixty}[2][]{%
	\bgroup%
	%! Set data
	\pgfkeys{/classycv/data/resume/Fourty Sixty/options/.cd, #1}
	\pgfkeys{/classycv/data/resume/Fourty Sixty/.cd, #2}%
	%! Define default components
	\@ifundefined{/classycv/components/resume/picture}{\classycvDefineComponent{/resume/picture}{\classycv@PutResumeFourtySixty@pictureComponent}}{}
	\@ifundefined{/classycv/components/resume/title}{\classycvDefineComponent{/resume/title}{\classycv@PutResumeFourtySixty@titleComponent}}{}
	\@ifundefined{/classycv/components/resume/content}{\classycvDefineComponent{/resume/title}{\classycv@PutResumeFourtySixty@titleComponent}}{}%	
	%! Set geometry and page style
	\loadgeometry{blank}%
	\pagestyle{blank}
	%! Set indentation to zero.
	\setlength{\parindent}{0pt}%
	%! 
	\begin{minipage}[t]{0.4\paperwidth}
%
%!todo: content
%
	\end{minipage}%
	%! put right page side
	\begin{minipage}[t]{0.6\paperwidth}%
    %! Put title
    \classycv@PutComponent{/resume/title}%
}{%
	\end{minipage}%
	%! Restore geometry, page style
	\clearpage
	\restoregeometry%
	\pagestyle{blank}%
	%! Restore indentation.
	\setlength{\parindent}{\classycv@parindent@default}%
	%! Clear page
	%!note `\clearpage` is necessary for geometry and page style to be applied
	%!ref: http://tex.stackexchange.com/a/115418
	\clearpage%
	\egroup%
}

\newcommand{\classycv@PutResumeFourtySixty@pictureComponent}{%
	%! Get data
	\pgfkeys{/classycv/data/resume/Fourty Sixty/picture/.get=\picture}%
	%! Put component
	\adjustbox{margin=10mm 0pt 0pt 10mm, minipage={\linewidth-10mm}}{%
		\ifnum\pdf@strcmp{\picture}{\@empty}=\z@%
		\else%
			\adjustbox{minipage={\linewidth}, bgcolor=light-gray}{%
				\begin{center}%
					\includegraphics[width=0.5\linewidth, keepaspectratio]{\picture}%
				\end{center}%
			}%
		\fi%
	}%
	\vspace*{24pt}\par%
}

\newcommand{\classycv@PutResumeFourtySixty@titleComponent}{%
	%! Get data
	\pgfkeys{/classycv/data/resume/Thirty Seventy/name/.get=\name}%
	%! Put component
	\Huge\color{accent-foreground}\MakeUppercase{\name}\par%
	%! Put delimiter
	\classycv@Resume@PutDelimiter{accent-foreground}%
}

%! Thirty Seventy resume format.
\newenvironment{classycv@PutResumeThirtySeventy}[2][]{%
	\bgroup%
	%
	%! Set data
	%
	\pgfkeys{/classycv/data/resume/Thirty Seventy/options/.cd, #1}
	\pgfkeys{/classycv/data/resume/Thirty Seventy/.cd, #2}%
	%
	%! Define default components
	%
	\@ifundefined{/classycv/components/resume/left}{\classycvDefineComponent{/resume/left}{\classycv@PutResumeThirtySeventy@leftComponent}}{}
	\@ifundefined{/classycv/components/resume/left/picture}{\classycvDefineComponent{/resume/left/picture}{\classycv@PutResumeThirtySeventy@left@pictureComponent}}{}
	\@ifundefined{/classycv/components/resume/left/personal data}{\classycvDefineComponent{/resume/left/personal data}{\classycv@PutResumeThirtySeventy@left@personalDataComponent}}{}
	\@ifundefined{/classycv/components/resume/left/contact data}{\classycvDefineComponent{/resume/left/contact data}{\classycv@PutResumeThirtySeventy@left@contactDataComponent}}{}
	\@ifundefined{/classycv/components/resume/left/extra data}{\classycvDefineComponent{/resume/left/extra data}{\classycv@PutResumeThirtySeventy@left@extraDataComponent}}{}
	%
	%! Set geometry and page style; clear page.
	%
	\loadgeometry{blank}%
	\pagestyle{blank}%
	\clearpage%
	%! Set indentation to zero.
	\setlength{\parindent}{0pt}%
	%! Draw left and right content boxes.
    \begin{tcolorbox}[%
        blanker%
        , leftupper=0.3\paperwidth%
        , boxsep=24pt%
        , width=\paperwidth%
        , height fixed for=all%
        , height fill=true%
        , breakable%
        , break at=\textheight%
        %! Put left page side as overlay.
        , overlay unbroken and first={%
        	\pgfkeys{%
				/classycv/data/resume/Thirty Seventy/options/.cd%
				, left background color/.get=\bg%
				, left style/.get=\style%
			}%
            \draw[use as bounding box, inner sep=0pt, outer sep=0pt, draw=none, fill=\bg] (0, 0) rectangle (0.3\paperwidth, \paperheight);%
            \node[draw=none, inner sep=0pt, outer sep=0pt, text width=0.3\paperwidth, below right=0pt and 0pt of current bounding box.north west]{%
            	\bgroup%
				\style%
				\classycv@PutComponent{/resume/left}%
				\egroup%
            };%
            \node[right=\dimexpr0.3\paperwidth-4pt\relax of current bounding box.west, minimum width=7.5pt, minimum height=15pt, inner sep=0pt, outer sep=0pt, diamond, draw=none, fill=\bg] {};
        }%
        , overlay middle and last={%
        	\pgfkeys{%
				/classycv/data/resume/Thirty Seventy/options/.cd%
				, left background color/.get=\bg%
				, left style/.get=\style%
			}%
            \draw[use as bounding box, inner sep=0pt, outer sep=0pt, draw=none, fill=\bg] (0, 0) rectangle (0.3\paperwidth, \paperheight);%
            \node[draw=none, inner sep=0pt, outer sep=0pt, text width=0.3\paperwidth, below right=0pt and 0pt of current bounding box.north west]{%
            	\bgroup%
				\style%
				\classycv@PutComponent{/resume/left}%
				\egroup%
            };%
            \node[right=\dimexpr0.3\paperwidth-4pt\relax of current bounding box.west, minimum width=7.5pt, minimum height=15pt, inner sep=0pt, outer sep=0pt, diamond, draw=none, fill=\bg] {};
        }%
    ]%
    %
    %! Put right page side.
	%
    \pgfkeys{/classycv/data/resume/Thirty Seventy/options/right basic style/.get=\rightStyle}%
    \bgroup%
    	\rightStyle%
}{%
	\egroup%
	\vfill%
	\end{tcolorbox}%
	%! Restore indentation.
	\setlength{\parindent}{\classycv@parindent@default}%
	\clearpage%
	\egroup%
}

%
%! Thirty Seventy resume format default components. 
%
\newcommand{\classycv@PutResumeThirtySeventy@leftComponent}{%
	\bgroup%
	%!todo refactor into components
	\pgfkeys{%
		/classycv/data/resume/Thirty Seventy/.cd%
		, picture/.get=\picture%
		, name/.get=\name%
		, title/.get=\title%
	}%
	\pgfkeys{%
		/classycv/data/resume/Thirty Seventy/options/.cd%
		, left basic style/.get=\leftStyle%
%		, left heading style/.get=\leftHeadingStyle%
%		, left entry style/.get=\leftEntryStyle%		
	}%

	\leftStyle%
	%! Put optional picture.
	\ifnum\pdf@strcmp{\@empty}{\picture}=\z@%
	\else%
		\classycv@PutComponent{/resume/left/picture}%
	\fi%
	%
	%! Put data.
	%
	\begin{center}%
		{\larger[3]\bfseries\name}\\
		\ifnum\pdf@strcmp{\@empty}{\title}=\z@\else\larger[2]\fontseries{l}\selectfont\title\\\fi%
	\end{center}%
	\begin{adjustbox}{minipage={\linewidth}, margin=12pt}%
		%
		%! Put personal data.
		%
		\classycv@PutComponent{/resume/left/personal data}%
		%
		%! Put contact data.
		%
		\classycv@PutComponent{/resume/left/contact data}%
		%
		%! Put extra data.
		%
		\classycv@PutComponent{/resume/left/extra data}%
	\end{adjustbox}%
	\egroup%
}

%
%! Thirty seventy resume picture component.
%
\newcommand{\classycv@PutResumeThirtySeventy@left@pictureComponent}{%
	\bgroup%
	\pgfkeys{/classycv/data/resume/Thirty Seventy/picture/.get=\picture}%
	\vspace*{16pt}\par%
	\tikz{%
		\draw[use as bounding box, draw=none] rectangle (\linewidth, 0.2\paperheight);%
		\begin{scope}
		    \clip (\dimexpr0.5\linewidth\relax, \dimexpr0.5\dimexpr\linewidth-16pt\relax) circle (\dimexpr0.5\dimexpr\linewidth-32pt\relax); 
		    \node[below right=16pt and 16pt of current bounding box.north west, inner sep=0pt] {\includegraphics[width=\linewidth-32pt\relax]{\picture}}; 
		\end{scope}
	}%
	\vspace*{2em}\par%	
	\egroup%
}
%
%! Left side bar personal data component.
%! This component contains personald data and is automatically generated from the arguments passed to the `\Resume` macro.
%
\newcommand{\classycv@PutResumeThirtySeventy@left@personalDataComponent}{%
	\bgroup%
%	\classycv@PutBar[skip above=2em, skip below=2em, strength=1pt]{accent-foreground!20!accent-background}%
	\pgfkeys{/classycv/data/resume/Thirty Seventy/personal data heading text/.get=\text}%
	%! Put picture
	%!todo refactor into components
	\pgfkeys{%
		/classycv/data/resume/Thirty Seventy/.cd%
%		, picture/.get=\picture%
%		, name/.get=\name%
%		, title/.get=\title%
%		, street/.get=\street%
%		, house/.get=\house%
%		, zipcode/.get=\zipcode%
%		, city/.get=\city%
		, birthdate/.get=\birthdate%
		, marital status/.get=\status%
		, nationality/.get=\nationality%
%		, phone/.get=\phone%
%		, mobile/.get=\mobile%
%		, email/.get=\email%
%		, website/.get=\website%
%		, personal data heading text/.get=\personalDataHeadingText%
%		, contact data heading text/.get=\contactDataHeadingText%
	}%
	\pgfkeys{%
		/classycv/data/resume/Thirty Seventy/options/.cd%
		, left header style/.get=\leftHeaderStyle%
		, left entry style/.get=\leftEntryStyle%		
%		, left additional personal data/.get=\additional%
	}%
	%
	%! Put personal data
	%
	\heading[%
		width=\dimexpr\linewidth-24pt\relax%
		, has label=yes%
		, label position=left%
		, label text={\faUser}%
		, skip above=2em%
		, skip below=0em%
		, label color=accent-foreground%
		, label text color=accent-background%
		, basic style=\leftHeaderStyle%
	] {\text}
	\begin{Table}[%
		skip above=1em%
		, skip below=0em%
		, column format={C{2em} L{\linewidth-24pt-2em}}%
		, basic style=\leftEntryStyle%
	]%
		\ifnum\pdf@strcmp{\birthdate}{\@empty}=\z@%
		\else%
			{\larger[2]\cmbrfamily\textborn}&\birthdate\\%
		\fi%
		\ifnum\pdf@strcmp{\status}{\@empty}=\z@%
		\else%
			{\larger[2]\cmbrfamily\textmarried}&\status\\%
		\fi%
		\ifnum\pdf@strcmp{\nationality}{\@empty}=\z@%
		\else%
			{\larger[2]\cmbrfamily\Mundus}&\nationality%
		\fi%
	\end{Table}%
	\egroup%
}
%
%! Left side bar contact data component.
%! This component contains contact data and is automatically generated from the arguments passed to the `\Resume` macro.
%
\newcommand{\classycv@PutResumeThirtySeventy@left@contactDataComponent}{%
	\pgfkeys{/classycv/data/resume/Thirty Seventy/contact data heading text/.get=\text}%
	\pgfkeys{%
		/classycv/data/resume/Thirty Seventy/.cd%
%		, picture/.get=\picture%
%		, name/.get=\name%
%		, title/.get=\title%
%		, street/.get=\street%
%		, house/.get=\house%
%		, zipcode/.get=\zipcode%
%		, city/.get=\city%
%		, birthdate/.get=\birthdate%
%		, marital status/.get=\status%
%		, nationality/.get=\nationality%
		, phone/.get=\phone%
		, mobile/.get=\mobile%
		, email/.get=\email%
		, website/.get=\website%
%		, personal data heading text/.get=\personalDataHeadingText%
%		, contact data heading text/.get=\contactDataHeadingText%
	}%
	\pgfkeys{%
		/classycv/data/resume/Thirty Seventy/options/.cd%
		, left header style/.get=\leftHeaderStyle%
		, left entry style/.get=\leftEntryStyle%		
%		, left additional contact data/.get=\additional%
	}%
	\heading[%
		width=\dimexpr\linewidth-24pt\relax%
		, has label=yes%
		, label position=left%
		, label text={\faComments}%
		, skip above=2em%
		, skip below=0em%
		, label color=accent-foreground%
		, label text color=accent-background%
		, basic style=\leftHeaderStyle%
	] {\text}
	\begin{Table}[%
		skip above=1em%
		, skip below=0em%
		, column format={C{2em} p{\linewidth-24pt-2em-3\tabcolsep}}%
		, basic style=\leftEntryStyle%
	]%	
		\ifnum\pdf@strcmp{\phone}{\@empty}=\z@\else{\larger[2]\cmbrfamily\Telefon}&\phone\\\fi%
		\ifnum\pdf@strcmp{\mobile}{\@empty}=\z@\else{\larger[2]\cmbrfamily\faMobile}&\mobile\\\fi%
		\ifnum\pdf@strcmp{\email}{\@empty}=\z@\else{\larger[2]\cmbrfamily\Letter}&\email\\\fi%
		\ifnum\pdf@strcmp{\website}{\@empty}=\z@\else{\larger[2]\cmbrfamily\ComputerMouse}&\website\fi%
	\end{Table}%
}
%
%! Left side bar extra component.
%! This component is added to the default components for personal and contact information in the left side bar of the thirty seventy format. It's empty by default.
%
\newcommand{\classycv@PutResumeThirtySeventy@left@extraDataComponent}{%
}%
%! Twenty Eighty resume format.
%
\newenvironment{classycv@PutResumeTwentyEighty}[2][]{%
	\bgroup%
	%! Set data
	\pgfkeys{/classycv/data/resume/Twenty Eighty/options/.cd, #1}
	\pgfkeys{/classycv/data/resume/Twenty Eighty/.cd, #2}%
	%! Define default components
	\@ifundefined{/classycv/components/resume/picture}{\classycvDefineComponent{/resume/picture}{\classycv@PutResumeTwentyEighty@pictureComponent}}{}
	\@ifundefined{/classycv/components/resume/information}{\classycvDefineComponent{/resume/information}{\classycv@PutResumeTwentyEighty@informationComponent}}{}
	\@ifundefined{/classycv/components/resume/contact}{\classycvDefineComponent{/resume/contact}{\classycv@PutResumeTwentyEighty@contactComponent}}{}
	\@ifundefined{/classycv/components/resume/extra}{\classycvDefineComponent{/resume/extra}{\classycv@PutResumeTwentyEighty@extraComponent}}{}%
	\@ifundefined{/classycv/components/resume/title}{\classycvDefineComponent{/resume/title}{\classycv@PutResumeTwentyEighty@titleComponent}}{}%
	%! Set geometry and page style; clear page.
	\loadgeometry{blank}%
	\pagestyle{blank}%
	\clearpage%
	%! Set indentation to zero.
	\setlength{\parindent}{0pt}%
    \begin{tcolorbox}[%
        blanker%
        , leftupper=0.2\paperwidth%
        , boxsep=24pt%
        , width=\paperwidth%
        , height fill=true%
        , height fixed for=all%
        , breakable%
        , break at=\textheight%
        %! Put left page side as overlay.
        , overlay unbroken and first={%
			\pgfkeys{%
				/classycv/data/resume/Twenty Eighty/options/.cd,%
				left background color/.get=\bg%
				left foreground color/.get=\fg%
			}%
            \draw[use as bounding box, inner sep=0pt, outer sep=0pt, draw=none, fill=\bg] (0, 0) rectangle (0.2\paperwidth, \paperheight);%
            \node[draw=none, inner sep=0pt, outer sep=0pt, text width=0.2\paperwidth, below right=0pt and 0pt of current bounding box.north west, text=\fg]{%
                \classycv@PutComponent{/resume/picture}%
                \classycv@PutComponent{/resume/information}%
                \classycv@PutComponent{/resume/contact}%
            };%
        }%
        , overlay middle and last={%
			\pgfkeys{%
				/classycv/data/resume/Twenty Eighty/options/.cd,%
				left background color/.get=\bg%
				left foreground color/.get=\fg%
			}%
            \draw[use as bounding box, inner sep=0pt, outer sep=0pt, draw=none, fill=\bg] (0, 0) rectangle (0.2\paperwidth, \paperheight);%
            \node[rotate=90, inner sep=0pt, outer sep=0pt, minimum width=\paperheight, minimum height=0.3\paperwidth, text width=\paperheight, anchor=north west, align=center, text=\fg] {%
                \pgfkeys{/classycv/data/resume/Thirty Seventy/name/.get=\name}%
                \bgroup%
                    \color{accent-foreground}\bfseries\fontsize{84pt}{92pt}\selectfont\name%
                \egroup%
            };%
        }%
    ]%
    %
    %! Put right page side.
    %
    %! Apply content style.
    \csname/classycv/style/resume/content\endcsname\relax%
    %! Put title
    \classycv@PutComponent{/resume/title}%
}{%
	\end{tcolorbox}%
	%! Restore indentation.
	\setlength{\parindent}{\classycv@parindent@default}%
	\egroup%
}

%
%! Twenty Eighty resume format default components. 
%

\newcommand{\classycv@PutResumeTwentyEighty@pictureComponent}{%
	\bgroup%
	%! put picture
	\pgfkeys{/classycv/data/resume/Twenty Eighty/picture/.get=\picture}%
	\ifnum\pdf@strcmp{\picture}{\@empty}=\z@%
	\else%
%		\vspace*{24pt}\par%
		\centerline{%
			\tcbox[boxsep=0pt, width=\linewidth, left=0pt, bottom=0pt, right=0pt, top=0pt, leftrule=0pt, bottomrule=0pt, rightrule=0pt, toprule=0pt, colframe=light-gray, sharp corners, standard jigsaw, opacityback=0]{%
				\tikz[opacity=0.95]{%
					\node{\includegraphics[width=\dimexpr0.75\linewidth\relax, keepaspectratio]{\picture}}%
				}%
			}%
		}%
		\vspace*{24pt}\par
	\fi%
	\egroup%
}

\newcommand{\classycv@PutResumeTwentyEighty@informationComponent}{%
	\bgroup%
	%! put personal data
	\pgfkeys{
		/classycv/data/resume/Twenty Eighty/.cd%
		, birthdate/.get=\birthdate%
		, marital status/.get=\status%
		, nationality/.get=\nationality%
	}%
	\adjustbox{margin=12pt 12pt 12pt 0pt, minipage=\linewidth-24pt}{%
		%! Style put before this component is being ignored and hence has to be restated here.
		\@ifundefined{/classycv/style/resume/information}{}{\csname/classycv/style/resume/information\endcsname}%
		%! Put the heading
		\classycv@tResume@heading[\raggedleft][\smallskip][]{\color{light-gray}\normalsize\faUser}%
		%! Put the delimiter
		\classycv@Resume@PutDelimiter[\linewidth][10pt][2pt]{accent-foreground}%
		%! Put content table
		\setlength{\tabcolsep}{0pt}%
		\begin{tabularx}{\linewidth}{M{24pt} X}%
			\ifnum\pdf@strcmp{\birthdate}{\@empty}=\z@\else{\cmrfamily\large\textborn}&\birthdate\\[0.5em]\fi%
			\ifnum\pdf@strcmp{\status}{\@empty}=\z@\else{\cmrfamily\large\textmarried}&\status\\[0.5em]\fi%
			\ifnum\pdf@strcmp{\nationality}{\@empty}=\z@\else{\large\Mundus}&\nationality\\\fi%
		\end{tabularx}%
		\setlength{\tabcolsep}{\classycv@tabcolsep@default}%
	}%
	\par%
	\egroup%
}

\newcommand{\classycv@PutResumeTwentyEighty@contactComponent}{%
	\bgroup%
	\pgfkeys{
		/classycv/data/resume/Twenty Eighty/.cd%
		, phone/.get=\phone%
		, mobile/.get=\mobile%
		, email/.get=\email%
		, website/.get=\website%
	}%
	%! put contact data
	\adjustbox{margin=12pt 12pt 12pt 0pt, minipage=\linewidth-24pt}{%
		%! Style put before this component is being ignored and hence has to be restated here.
		\@ifundefined{/classycv/style/resume/information}{}{\csname/classycv/style/resume/information\endcsname}%
		%! Put heading
		\classycv@Resume@PutHeading[\raggedleft][][]{\color{light-gray}\normalsize\faCommentsO}%
		%! Put delimiter
		\classycv@Resume@PutDelimiter[\linewidth][10pt][2pt]{accent-foreground}%
		%! Put content table
		\setlength{\tabcolsep}{0pt}
		\begin{tabularx}{\linewidth}{M{24pt} X}
			\ifnum\pdf@strcmp{\phone}{\@empty}=\z@\else{\large\Telefon}&\phone\\[0.5em]\fi%
			\ifnum\pdf@strcmp{\mobile}{\@empty}=\z@\else{\large\faMobile}&\mobile\\[0.5em]\fi%
			\ifnum\pdf@strcmp{\email}{\@empty}=\z@\else{\large\Letter}&\email\\[0.5em]\fi%
			\ifnum\pdf@strcmp{\website}{\@empty}=\z@\else{\large\ComputerMouse}&\website\fi%
		\end{tabularx}%
		\setlength{\tabcolsep}{\classycv@tabcolsep@default}
	}%
	\par%
	\egroup%
}

\newcommand{\classycv@PutResumeTwentyEighty@extraComponent}{%
\relax%
}

\newcommand{\classycv@PutResumeTwentyEighty@titleComponent}{%
	%! Get data
	\pgfkeys{/classycv/data/resume/Thirty Seventy/name/.get=\name}%
	%! Put component
	\Huge\color{accent-foreground}\MakeUppercase{\name}\par%
	%! Put delimiter
	\classycv@Resume@PutDelimiter{accent-foreground}%
}

%
%! Attachment header.
%
\newcommand{\classycv@attachment@headerComponent}{%
}

\newcommand{\classycv@attachment@footerComponent}{%
	\bgroup%
	\pgfkeys{%
		/classycv/data/attachment/.cd%
		, submitter name/.get=\submitterName%
		, attachment name/.get=\attachmentName%
	}%
	\pgfkeys{%
		/classycv/data/attachment/options/.cd%
		, has page counter/.get=\hasPageCounter%
		, background color/.get=\bg%
		, foreground color/.get=\fg%
		, text style/.get=\textStyle%
	}%
	\tikz{%
		\draw[use as bounding box, draw=none] rectangle (\paperwidth, 12.5mm);%
		\node[diamond, draw=none, minimum width=15pt, minimum height=7.5pt, inner sep=0pt, outer sep=0pt, below=0pt of current bounding box.north, fill=\bg] (mark) {};%
		\node[minimum width=\paperwidth, text width=\paperwidth, minimum height=11.75mm, inner sep=0pt, outer sep=0pt, below right=3.25pt and 0pt of current bounding box.north west, fill=\bg]{%
			\hspace*{24pt}\begin{tabular}{m{0.9\dimexpr\linewidth-24pt\relax-\tabcolsep} m{0.1\dimexpr\linewidth-24pt\relax-\tabcolsep}}%
				\ifnum\pdf@strcmp{\@empty}{\attachmentName}=\z@\else%
					\textStyle{\bfseries\faFilesO}~\attachmentName%
				\fi%
				& \ifnum\pdf@strcmp{yes}{\hasPageCounter}=\z@%
					\setcounter{classycv@variables@counterI}{\getpagerefnumber{attachment-\theclassycv@attachmentCounter-first-page}}%
					\setcounter{classycv@variables@counterII}{\getpagerefnumber{attachment-\theclassycv@attachmentCounter-last-page}}%
					\textStyle\number\numexpr1 + \thepage - \theclassycv@variables@counterI\relax~|~\number\numexpr\theclassycv@variables@counterII-\theclassycv@variables@counterI\relax%
				\fi%
			\end{tabular}%
			\hspace*{12pt}%
		};%
	}%
	\egroup%
}

\makeatother
	
%!%!%!%!%!%!
% settings %
%!%!%!%!%!%!

% % % % % % % % % % % 
% tabularx settings %
% % % % % % % % % % %

%! Centered fixed width column.
%!ref http://tex.stackexchange.com/a/238023
\newcolumntype{C}[1]{>{\centering\arraybackslash}p{#1}}
\newcolumntype{L}[1]{>{\raggedright\arraybackslash}p{#1}}
\newcolumntype{R}[1]{>{\raggedleft\arraybackslash}p{#1}}
\newcolumntype{M}[1]{>{\centering\arraybackslash}m{#1}}

% % % % % % % % % % % % 
% classycv settings  %
% % % % % % % % % % % %
\makeatletter

%
%! settings
%
\pgfkeys{%
	/classycv/data/settings/cover letter/.cd%
	, format/.initial=\classycv@FORMAT@COVERLETTER@DINLETTERA%
	, format/.default=\classycv@FORMAT@COVERLETTER@DINLETTERA%
}

%
%! `\classycv@PutBar` options
%
\pgfkeys{%
	/classycv/data/put bar/options/.cd%
	, width/.initial=\dimexpr\linewidth-24pt\relax%
	, width/.default=\dimexpr\linewidth-24pt\relax%
	, height/.initial=1em%
	, height/.default=1em%
	, color/.initial=accent-foreground%
	, color/.default=accent-foreground%
	, strength/.initial=2pt%
	, strength/.default=2pt%
%	, basic style/.initial={\robotofamily\normalsize\fontseries{l}\selectfont\color{accent-foreground}}%
%	, basic style/.default={\robotofamily\normalsize\fontseries{l}\selectfont\color{accent-foreground}}%
	, skip above/.initial=1em%
	, skip above/.default=1em%	
	, skip below/.initial=2em%
	, skip below/.default=2em%	
}

%
%! `\classycv@PutProgressBar` options
%
\pgfkeys{%
	/classycv/data/put progress bar/options/.cd%
	, height/.initial=1em%
	, height/.default=1em%
	, background color/.initial=accent-background!25!nearly-white%
	, background color/.default=accent-background!25!nearly-white%
	, foreground color/.initial=accent-background%
	, foreground color/.default=accent-background%	
	, bar width/.initial=\linewidth%
	, bar width/.default=\linewidth%
	, border width/.initial=0pt
	, border width/.default=0pt	
	, border color/.initial=none%
	, border color/.default=none%
	, has label/.initial=no%
	, has label/.default=no%
	, label width/.initial=0pt%
	, label width/.default=0pt%
	, label position/.initial=left%
	, label position/.default=left%
	, label text/.initial=\@empty%
	, label text/.default=\@empty%
	, label font/.initial=\normalsize%
	, label font/.default=\normalsize%
	, label text align/.initial=left%
	, label text align/.default=left%
	, label color/.initial=accent-background%
	, label color/.default=accent-background%
	, skip above/.initial=1em%
	, skip above/.default=1em%	
	, skip below/.initial=2em%
	, skip below/.default=2em%	
	, skip between/.initial=4pt%
	, skip between/.default=4pt%
}

\pgfkeys{%
	/classycv/data/put semicircle/options/.cd%
	, size/.initial=2em%
	, size/.default=2em%
	, strength/.initial=2pt%
	, strength/.default=2pt%
	, line color/.initial=accent-background%
	, line color/.default=accent-background%
	, fill color/.initial=white!0%
	, fill color/.default=white!0%
	, has label/.initial=no%
	, has label/.default=no%
	, label text/.initial=\@empty%
	, label text/.default=\@empty%
	, label font/.initial=\normalsize%
	, label font/.default=\normalsize%
	, label color/.initial=accent-background%
	, label color/.default=accent-background%
	, draw complement/.initial=yes%
	, draw complement/.default=yes%
	, complement line color/.initial=light-gray%
	, complement line color/.default=light-gray%
	, draw glow/.initial=no%
	, draw glow/.default=no%
}

%
%! `\classycv@PutDoughnutChart` options.
%
\pgfkeys{%
	/classycv/data/put doughnut chart/options/.cd%
	, size/.initial=2em%
	, size/.default=2em%
	, strength/.initial=2pt%
	, strength/.default=2pt%
%	, line color/.initial=accent-background%
%	, line color/.default=accent-background%
	, label size/.initial=1em%
	, label size/.default=1em%
	, label shape/.initial=circle%
	, label shape/.default=circle%
	, label line color/.initial=white%
	, label line color/.default=white%
	, label fill color/.initial=white%
	, label fill color/.default=white%
	, label text color/.default=dark-gray%
	, label text color/.initial=dark-gray%
	, basic style/.initial={\robotofamily\tiny\fontseries{l}\selectfont\color{white}}%
	, basic style/.default={\robotofamily\tiny\fontseries{l}\selectfont\color{white}}%
}

%
%!tmp
%
\iffalse
\pgfkeys{%
	/classycv/data/put star/options/.cd%
	, size/.initial=2em%
	, size/.default=2em%
}
\fi

%
%! `\classycv@PutHeading` options
%
\pgfkeys{%
	/classycv/data/put heading/options/.cd%
	, width/.initial=\dimexpr\linewidth-24pt\relax%
	, width/.default=\dimexpr\linewidth-24pt\relax%
	, height/.initial=2em%
	, height/.default=2em%
	, has label/.initial=no%
	, has label/.default=no%
	, label shape/.initial=circle%
	, label shape/.default=circle%
	, label width/.initial=1.25em%
	, label width/.default=1.25em%
	, label color/.initial=accent-background%
	, label color/.default=accent-background%
	, label frame color/.initial=accent-foreground%
	, label frame color/.default=accent-foreground%
	, label frame width/.initial=0pt%
	, label frame width/.default=0pt%
	, label inner sep/.initial=4pt%
	, label inner sep/.default=4pt%
	, label text color/.initial=accent-foreground%
	, label text color/.default=accent-foreground%
	, label position/.initial=left%
	, label position/.default=left%
	, label options/.initial=\@empty%
	, label options/.default=\@empty%
	, label text/.initial=\@empty%
	, label text/.default=\@empty%
	, basic style/.initial={\flafamily\larger[2]\bfseries\color{accent-foreground}}%
	, basic style/.default={\flafamily\larger[2]\bfseries\color{accent-foreground}}%
	, skip above/.initial=1em%
	, skip above/.default=1em%	
	, skip below/.initial=2em%
	, skip below/.default=2em%
	, skip between/.initial=1em%
	, skip between/.default=1em%	
}

%
%! `\classycv@PutTable` options
%
\pgfkeys{%
	/classycv/data/put table/options/.cd%
	, width/.initial=\dimexpr\linewidth-24pt\relax%
	, width/.default=\dimexpr\linewidth-24pt\relax%
	, basic style/.initial={\robotofamily\normalsize\fontseries{l}\selectfont\color{accent-background}}%
	, basic style/.default={\robotofamily\normalsize\fontseries{l}\selectfont\color{accent-background}}%
	, column format/.initial={R{0.2\dimexpr\linewidth-48pt} L{0.8\dimexpr\linewidth-48pt}}%
	, column format/.default={l l}%
	, stretch/.initial={1.0}%
	, stretch/.default={1.0}%
%	, alignment/.initial=c%
%	, alignment/.default=c%
	, skip above/.initial=1em%
	, skip above/.default=1em%	
	, skip below/.initial=2em%
	, skip below/.default=2em%	
}

%
%! DIN 5008 A letter data
%
\pgfkeys{%
	/classycv/data/cover letter/DIN 5008 A/options/.cd%
	, has body separator/.initial=yes%
	, has body separator/.default=yes%
	, has footer separator/.initial=yes%
	, has footer separator/.default=yes%
	, has page counter/.initial=yes%
	, has page counter/.default=yes%
	, header repeat/.initial=no%
	, header repeat/.default=no%
	, header basic style/.initial={\flafamily\color{nearly-white}}%
	, header basic style/.default={\flafamily\color{nearly-white}}%
	, header name style/.initial={\Large\mdseries}%
	, header name style/.default={\Large\mdseries}%
	, header address style/.initial={\footnotesize\fontseries{l}\selectfont}%
	, header address style/.default={\footnotesize\fontseries{l}\selectfont}%
	, header details style/.initial={\footnotesize\fontseries{l}\selectfont}%
	, header details style/.default={\footnotesize\fontseries{l}\selectfont}%
	, header background color/.initial=accent-background%
	, header background color/.default=accent-background%
	, header foreground color/.initial=accent-foreground%
	, header foreground color/.default=accent-foreground%
	, header line color/.initial=accent-background%
	, header line color/.default=accent-background%
	, recipient information line color/.initial=medium-gray%
	, recipient information line color/.default=medium-gray%
	, recipient information padding/.initial=1em%
	, recipient information padding/.default=1em%
	, recipient information basic style/.initial={\fontsize{3.75mm}{3.75mm}\selectfont}%
	, recipient information basic style/.default={\fontsize{3.75mm}{3.75mm}\selectfont}%
	, recipient information organisation style/.initial={\robotofamily\MakeUppercase}%
	, recipient information organisation style/.default={\robotofamily\MakeUppercase}%
	, recipient information name style/.initial={\robotofamily\fontseries{b}\selectfont}%
	, recipient information name style/.default={\robotofamily\fontseries{b}\selectfont}%
	, recipient information position style/.initial={\itshape}%
	, recipient information position style/.default={\itshape}%
	, recipient information address style/.initial={\robotofamily\fontseries{m}}%
	, recipient information address style/.default={\robotofamily\fontseries{m}}%
	, submitter information line color/.initial=medium-gray%
	, submitter information line color/.default=medium-gray%
	, submitter information padding/.initial=1em%
	, submitter information padding/.default=1em%
	, submitter information basic style/.initial={\fontsize{3.75mm}{3.75mm}\selectfont}%
	, submitter information basic style/.default={\fontsize{3.75mm}{3.75mm}\selectfont}%
	, date line style/.initial={\robotofamily\normalsize\color{medium-gray}}%
	, date line style/.default={\robotofamily\normalsize\color{medium-gray}}%
	, subject line style/.initial={\robotofamily\normalsize\bfseries}%
	, subject line style/.default={\robotofamily\normalsize\bfseries}%
	, opening line style/.initial={\lmrfamily\normalsize}%
	, opening line style/.default={\lmrfamily\normalsize}%
	, content style/.initial={\lmrfamily\normalsize}%
	, content style/.default={\lmrfamily\normalsize}%
	, closing line style/.initial={\lmrfamily\normalsize}%
	, closing line style/.default={\lmrfamily\normalsize}%
	, signature basic style/.initial={\robotofamily\fontseries{l}\selectfont\normalsize}%
	, signature basic style/.default={\robotofamily\fontseries{l}\selectfont\normalsize}%	
	, signature name line style/.initial=%
	, signature name line style/.default=%
	, signature position line style/.initial=%
	, signature position line style/.default=%
	, signature organisation line style/.initial={\MakeUppercase}%
	, signature organisation line style/.default={\MakeUppercase}%
%	, attachments style/.initial={\robotofamily\fontseries{l}\selectfont\normalsize\color{medium-gray}}%
%	, attachments style/.default={\robotofamily\fontseries{l}\selectfont\normalsize\color{medium-gray}}%
	, footer style/.initial={\robotofamily\small\mdseries\color{medium-gray}}
	, footer style/.default={\robotofamily\small\mdseries\color{medium-gray}}
}

\pgfkeys{%
	/classycv/data/cover letter/DIN 5008 A/submitter/.cd%
	, title/.initial=\@empty%
	, title/.default=\@empty%
	, name/.initial=\@empty%
	, name/.default=\@empty%
	, organisation/.initial=\@empty%
	, organisation/.default=\@empty%
	, position/.initial=\@empty%
	, position/.default=\@empty%
	, street/.initial=\@empty%
	, street/.default=\@empty%
	, house/.initial=\@empty%
	, house/.default=\@empty%
	, zipcode/.initial=\@empty%	
	, zipcode/.default=\@empty%	
	, city/.initial=\@empty%
	, city/.default=\@empty%	
	, country/.initial=\@empty%
	, country/.default=\@empty%
	, phone/.initial=\@empty%
	, phone/.default=\@empty%	
	, mobile/.initial=\@empty%
	, mobile/.default=\@empty%
	, fax/.initial=\@empty%
	, fax/.default=\@empty%
	, email/.initial=\@empty%
	, email/.default=\@empty%	
	, website/.initial=\@empty%
	, website/.default=\@empty%
	, sign/.initial=\@empty%
	, sign/.default=\@empty%
	, reply sign/.initial=\@empty%
	, reply sign/.default=\@empty%
	, original sign/.initial=\@empty%
	, original sign/.default=\@empty%	
	, date/.initial=\@empty%
	, date/.default=\@empty%	
	, reply message date/.initial=\@empty%
	, reply message date/.default=\@empty%	
	, original message date/.initial=\@empty%
	, original message date/.default=\@empty%
	, attachments/.initial=\@empty%
	, attachments/.default=\@empty%	
}

\pgfkeys{%
	/classycv/data/cover letter/DIN 5008 A/recipient/.cd%
	, rta/.initial=\@empty%
	, title/.initial=\@empty%
	, name/.initial=\@empty%
	, organisation/.initial=\@empty%
	, position/.initial=\@empty%
	, street/.initial=\@empty%
	, house/.initial=\@empty%
	, zipcode/.initial=\@empty%	
	, city/.initial=\@empty%
	, country/.initial=\@empty%
}	

\pgfkeys{%
	/classycv/data/cover letter/DIN 5008 A/.cd%
	, date/.initial=\today%
	, date/.default=\today%
	, subject/.initial=\@empty%
	, subject/.default=\@empty%
	, opening/.initial=\@empty%
	, opening/.default=\@empty%
	, closing/.initial=\@empty%
	, closing/.default=\@empty%
}%

%
%! resume data
%
\pgfkeys{%
	/classycv/data/settings/resume/.cd%
	, format/.initial=\classycv@FORMAT@RESUME@THIRTYSEVENTY%
	, format/.default=\classycv@FORMAT@RESUME@THIRTYSEVENTY%	
}

%
%! Fourty Sixty resume data
%
\pgfkeys{%
	/classycv/data/resume/Fourty Sixty/options/.cd%
	, left background color/.initial=accent-background
	, left background color/.default=accent-background
	, left foreground color/.initial=nearly-white
	, left foreground color/.default=nearly-white
}

\pgfkeys{%
	/classycv/data/resume/Fourty Sixty/.cd%
	, picture/.initial=\@empty%
	, name/.initial=\@empty%
	, birthdate/.initial=\@empty%
	, marital status/.initial=\@empty%
	, nationality/.initial=\@empty%
	, phone/.initial=\@empty%
	, mobile/.initial=\@empty%
	, email/.initial=\@empty%
	, website/.initial=\@empty%
}

%
%! Thirty Seventy resume data
%
\pgfkeys{%
	/classycv/data/resume/Thirty Seventy/.cd%
	, picture/.initial=\@empty%
	, picture/.default=\@empty%
	, name/.initial=\@empty%
	, name/.default=\@empty%
	, title/.initial=\@empty%
	, title/.default=\@empty%
	, street/.initial=\@empty%
	, street/.default=\@empty%
	, house/.initial=\@empty%
	, house/.default=\@empty%
	, zipcode/.initial=\@empty%
	, zipcode/.default=\@empty%
	, city/.initial=\@empty%
	, city/.default=\@empty%
	, country/.initial=\@empty%
	, country/.default=\@empty%
	, birthdate/.initial=\@empty%
	, birthdate/.default=\@empty%
	, marital status/.initial=\@empty%
	, marital status/.default=\@empty%
	, nationality/.initial=\@empty%
	, nationality/.default=\@empty%
	, phone/.initial=\@empty%
	, phone/.default=\@empty%
	, mobile/.initial=\@empty%
	, mobile/.default=\@empty%
	, email/.initial=\@empty%
	, email/.default=\@empty%
	, website/.initial=\@empty%
	, website/.default=\@empty%
	, personal data heading text/.initial=\@empty%
	, personal data heading text/.default=\@empty%
	, contact data heading text/.initial=\@empty%
	, contact data heading text/.default=\@empty%
	, submitter information basic style/.initial={}%
	, submitter information basic style/.default={}%
}

\pgfkeys{%
	/classycv/data/resume/Thirty Seventy/options/.cd%
	, left basic style/.initial={\robotofamily\fontseries{l}\selectfont\small\color{accent-foreground}}%
	, left basic style/.default={\robotofamily\fontseries{l}\selectfont\small\color{accent-foreground}}%
	, left background color/.initial=accent-background%
	, left background color/.default=accent-background%
	, left foreground color/.initial=nearly-white%
	, left foreground color/.default=nearly-white%
%	, left name style/.initial={\flafamily\larger[2]\mdseries\scshape\color{accent-foreground}}%
%	, left name style/.default={\flafamily\larger[2]\mdseries\scshape\color{accent-foreground}}%	
%	, left title style/.initial={\flafamily\fontseries{l}\selectfont\larger\color{accent-foreground}}%
%	, left title style/.default={\flafamily\fontseries{l}\selectfont\larger\color{accent-foreground}}%	
	, left address style/.initial={\flafamily\fontseries{l}\selectfont\larger\color{accent-foreground}}%
	, left address style/.default={\flafamily\fontseries{l}\selectfont\larger\color{accent-foreground}}%
	, left header style/.initial={\flafamily\mdseries\normalsize\color{white}}%
	, left header style/.default={\flafamily\mdseries\normalsize\color{white}}%
	, left header skip before/.initial={\bigskip}%
	, left header skip before/.default={\bigskip}%
	, left entry style/.initial={\robotofamily\fontseries{l}\selectfont\small\color{white}}%
	, left entry style/.default={\robotofamily\fontseries{l}\selectfont\small\color{white}}%
	, left entry skip above/.initial={}%
	, left entry skip above/.default={}%
	, left entry skip below/.initial={\smallskip}%
	, left entry skip below/.default={\smallskip}%
%	, left additional personal data/.initial=\@empty%
%	, left additional personal data/.default=\@empty%
%	, left additional contact data/.initial=\@empty%
%	, left additional contact data/.default=\@empty%
	, right basic style/.initial={\robotofamily\fontseries{l}\selectfont\normalsize\color{black}}%
	, right basic style/.default={\robotofamily\fontseries{l}\selectfont\normalsize\color{black}}%	
%	, content lines style/.initial={\lmrfamily\larger}%
%	, content lines style/.default={\lmrfamily\fontseries{l}\selectfont\larger}%

}

%
%! Twenty Eighty resume data
%
\pgfkeys{%
	/classycv/data/resume/Twenty Eighty/options/.cd%
	, left background color/.initial=accent-background
	, left background color/.default=accent-background
	, left foreground color/.initial=nearly-white
	, left foreground color/.default=nearly-white
}

\pgfkeys{%
	/classycv/data/resume/Twenty Eighty/.cd%
	, picture/.initial=\@empty%
	, name/.initial=\@empty%
	, birthdate/.initial=\@empty%
	, marital status/.initial=\@empty%
	, nationality/.initial=\@empty%
	, phone/.initial=\@empty%
	, mobile/.initial=\@empty%
	, email/.initial=\@empty%
	, website/.initial=\@empty%
}

%
%! Attachment data
%
\pgfkeys{%
	/classycv/data/attachment/.cd%
	, submitter name/.initial=\@empty%
	, attachment name/.initial=\@empty%
}

\pgfkeys{%
	/classycv/data/attachment/options/.cd%
	, has page counter/.initial=yes%
	, background color/.initial=accent-background%
	, background color/.default=accent-background%
	, foreground color/.initial=accent-foreground%
	, foreground color/.default=accent-foreground%
	, text style/.initial={\robotofamily\color{white}}%
	, text style/.default={\robotofamily\color{white}}%
}

%
%!note define page geometry styles
%

%! default geometry
\geometry{}
\savegeometry{default}

%! blank page
\newgeometry{%
	%! ignore header, footer, margin par
	noheadfoot%
	, nomarginpar%
	, ignoreall%
	, width=\paperwidth%
	, height=\paperheight%
%	, headheight=0pt%
%	, headsep=0pt%
%	, footskip=0pt%
%	, tmargin=0pt%
%	, bmargin=0pt%
}
\savegeometry{blank}

%! DIN 5008 A letter format
%!ref http://tex.stackexchange.com/a/111380 (setting footer height)
%!ref[Wikipedia] https://de.wikipedia.org/wiki/DIN_5008#/media/File:DIN_5008,_Form_A.svg
\newgeometry{%
	includeheadfoot%
	, nomarginpar%
%	, top=0mm%
	, headheight=27mm%
	, headsep=6pt%
	, foot=4.38mm%
%	, footskip=\dimexpr4.38mm+\ht\strutbox\relax
	, footskip=0mm
	, tmargin=0mm%
	%!note guesstimation from drawing [Wikipedia]
	, bmargin=42mm
	, width=\the\paperwidth%
	, height=\the\paperheight%
}
\savegeometry{din-5008-a}

%! Attachment geometry.
\newgeometry{%
	includeheadfoot%
	, nomarginpar%
%	, top=0mm%
	, headheight=0pt%
	, headsep=0pt%
%	, foot=4.38mm%
%	, footskip=\dimexpr4.38mm+\ht\strutbox\relax
	, foot=0pt%
	, footskip=0mm%
	, tmargin=0mm%
	, bmargin=12.5mm%
	, width=\the\paperwidth%
	, height=\the\paperheight%
}
\savegeometry{attachment}

% % % % % % % % % % %
% titleps settings %
% % % % % % % % % % %
\newpagestyle{blank}{%
	\setheadrule{0pt}%
	\setfootrule{0pt}%
	\sethead{}{}{}%
	\setfoot{}{}{}%
}

\newpagestyle{cover-letter}{%
	%! remove header rule and footer rule
	\setheadrule{0pt}%
	\setfootrule{0pt}%
	\sethead{%
		%! Increase the cover letter page counter
		\stepcounter{classycv@coverLetterPageCounter}%	
		\classycv@PutComponent{/cover letter/header}%
	}{}{}%
	\setfoot{%
		\classycv@PutComponent{/cover letter/footer}%
	}{}{}%
}

\newpagestyle{attachment}{%
	%! remove header rule and footer rule
	\setheadrule{0pt}%
	\setfootrule{0pt}%
	\sethead{}{}{}%
	\setfoot{%
		\classycv@PutComponent{/attachment/footer}%
	}{}{}%
}
	
% % % % % % % % %
% tikz settings %
% % % % % % % % %

\usetikzlibrary{positioning, calc, shapes, svg.path, shadows}
\pgfdeclarelayer{background}
\pgfdeclarelayer{overlay 1}
\pgfdeclarelayer{overlay 2}
\pgfsetlayers{background,main,overlay 1,overlay 2}

% % % % % % % % % % % %
% tcolorbox settings  %
% % % % % % % % % % % %
\tcbuselibrary{breakable}
\tcbuselibrary{skins}

%!%!%!%!%!%!%
% handlers  %
%!%!%!%!%!%!%
\AtEndDocument{%
\cleardoublepage%
\clearpage%
\newpage%
\pagestyle{empty}%
\vspace*{\fill}%
	\begin{center}
		\Huge\flafamily\fontseries{l}\selectfont Made with package \textcolor{accent-background}{\bfseries classycv} for \LaTeX2e
	\end{center}%
\vspace*{\fill}%
}
