# Signals and Systems Lecture Conventions

This document outlines all conventions, standards, and patterns used across the Signals and Systems lecture series to ensure consistency and maintainability.

## Document Structure

### File Naming
- **Lecture files**: `lecXX.tex` where XX is the lecture number (01, 02, 03, etc.)
- **Figure files**: `fig_[descriptive_name].tex` in `figures/lecXX/` folders
- **Figure naming pattern**: 
  - `fig_ct_[signal_type]` for continuous-time signals
  - `fig_dt_[signal_type]` for discrete-time signals
  - `fig_[concept_name]` for general concepts
  - `fig_[example_name]` for specific examples

### Document Class and Packages
```latex
\documentclass[11pt]{article}

% Standard package set (in order):
\usepackage{amsmath,amssymb,mathtools}
\usepackage[margin=1in]{geometry}
\usepackage{enumitem}
\usepackage{xcolor}
\usepackage{microtype}
\usepackage{graphicx}
\usepackage{tikz,float}
\usepackage{subcaption}
\usepackage{amsthm}
\usepackage{hyperref}
```

### TikZ Setup
```latex
\usetikzlibrary{shapes.geometric, arrows.meta, positioning, calc, decorations.markings}
\tikzset{
	block/.style={rectangle, draw, text width=6em, text centered, rounded corners, minimum height=10mm},
	sum/.style={circle, draw, node distance=1.5cm},
	line/.style={draw, -{Stealth[length=2.5mm, width=1.5mm]}}
}
```

### PGFPlots Setup
```latex
\usepackage{pgfplots}
\usepgfplotslibrary{groupplots}
\pgfplotsset{compat=1.18}

% Global custom axis style for consistency
\pgfplotsset{
	myaxes/.style={
		axis lines=middle,
		grid=both,
		minor grid style={gray!15},
		major grid style={gray!35},
		tick align=outside,
		tick style={black},
		xlabel style={yshift=3pt, anchor=north},
		ylabel style={yshift=-3pt, anchor=south},
		clip=false
	},
	myplotstyle/.style={
		width=14cm,
		height=7cm,
		axis lines=middle,
		axis line style={-Stealth},
		grid=both,
		minor tick num=1,
		major grid style={draw=gray!30},
		minor grid style={draw=gray!15},
		tick label style={font=\small, fill=white, inner sep=1.5pt},
		xlabel={$t$},
		ylabel={$x(t)$},
		xlabel style={anchor=north east, font=\small},
		ylabel style={anchor=south east, font=\small},
		samples=401,
	}
}
```

### Theorem Environments
```latex
\newtheoremstyle{mynote}
{6pt}      % Space above
{6pt}      % Space below
{}         % Body font (normal, not italic)
{}         % Indent amount
{\bfseries}  % Theorem head font
{.}        % Punctuation after theorem head
{.5em}     % Space after theorem head
{}         % Theorem head spec
\theoremstyle{mynote}
\newtheorem{definition}{Definition}
\newtheorem{proposition}{Proposition}
\newtheorem{example}{Example}
\newtheorem{remark}{Remark}
\newtheorem{theorem}{Theorem}
\newtheorem{corollary}{Corollary}
```

### Mathematical Macros
```latex
\newcommand{\T}{\mathcal{T}}        % System operator
\newcommand{\R}{\mathbb{R}}         % Real numbers
\newcommand{\Z}{\mathbb{Z}}         % Integers
\newcommand{\C}{\mathbb{C}}         % Complex numbers
\newcommand{\conv}{\ast}            % Convolution operator
\newcommand{\dt}{\mathrm{d}t}       % Differential dt
\newcommand{\dd}{\mathrm{d}}        % Differential d
\newcommand{\imp}{\delta}           % Impulse function
\newcommand{\sinc}[1]{\frac{\sin(\pi #1)}{\pi #1}}  % Sinc function
```

## Document Layout

### Title Block
```latex
% Reset figure counter for this lecture
\renewcommand{\thefigure}{X.\arabic{figure}}

% --- TITLE BLOCK ---
\thispagestyle{empty}
\noindent
\begin{tabular*}{\textwidth}{l @{\extracolsep{\fill}} r}
	\textbf{Signals and Systems} & \textbf{Lecture X} \\
	\textit{Ahmed Rabei} & \textit{Fall 2025} \\
\end{tabular*}
\hrule
\vspace{0.4cm}
\begin{center}
	\Large\textbf{Lecture X: [Lecture Title]}
\end{center}
\vspace{0.4cm}
```

### Section Structure
1. **Reference** - Textbook reference
2. **Review of Lecture X-1** - Previous lecture summary
3. **Main sections** - Numbered as X.1, X.2, etc.
4. **Subsections** - Numbered as X.1.1, X.1.2, etc.
5. **Summary and Next Lecture** - Key takeaways and preview

### Reference Section
```latex
\section*{Reference}
	Oppenheim \& Willsky, \textit{Signals and Systems}, Chapter X, Sections X.X--X.X
```

### Review Section
```latex
\section*{Review of Lecture X-1}
	\begin{itemize}[noitemsep]
		\item [Previous lecture key point 1]
		\item [Previous lecture key point 2]
		\item [Previous lecture key point 3]
		\item [Previous lecture key point 4]
	\end{itemize}
```

## Content Conventions

### Mathematical Notation
- **Continuous-time signals**: `x(t)`, `y(t)`, `h(t)`
- **Discrete-time signals**: `x[n]`, `y[n]`, `h[n]`
- **System operator**: `\T\{\cdot\}`
- **Convolution**: `x(t) \conv h(t)` or `(x \conv h)(t)`
- **Fourier transform**: `X(j\omega)`, `H(j\omega)`
- **Fourier series coefficients**: `a_k`, `b_k`
- **Time variables**: `t` for continuous, `n` for discrete
- **Frequency variables**: `\omega` for angular frequency, `f` for frequency in Hz

### List Formatting
- Use `\begin{itemize}[noitemsep]` for compact lists
- Use `\begin{enumerate}[noitemsep]` for numbered lists
- Use `\begin{itemize}` with `\item[]` for example lists with empty bullets

### Theorem and Definition Formatting
- Always use the custom theorem style
- Include clear, concise statements
- Use appropriate theorem type (definition, proposition, theorem, example, remark)

### Example Formatting
```latex
\begin{example}
	[Example description]
	
	\textbf{Solution:}
	[Solution steps]
	
	Therefore: [Final result]
\end{example}
```

## Figure Conventions

### Figure Structure
```latex
\begin{figure}[H]
	\centering
	\input{figures/lecXX/fig_[figure_name].tex}
	\caption{[Descriptive caption]}
	\label{fig:[figure_label]}
\end{figure}
```

### Subfigure Structure
```latex
\begin{figure}[H]
	\centering
	\begin{subfigure}[b]{0.48\textwidth}
		\centering
		\input{figures/lecXX/fig_[subfigure1_name].tex}
		\caption{[Subfigure 1 caption]}
		\label{fig:[subfigure1_label]}
	\end{subfigure}
	\hfill
	\begin{subfigure}[b]{0.48\textwidth}
		\centering
		\input{figures/lecXX/fig_[subfigure2_name].tex}
		\caption{[Subfigure 2 caption]}
		\label{fig:[subfigure2_label]}
	\end{subfigure}
	\caption{[Overall figure caption]}
	\label{fig:[overall_figure_label]}
\end{figure}
```

### Figure Naming Patterns
- **Signal plots**: `fig_ct_[signal_type]`, `fig_dt_[signal_type]`
- **System diagrams**: `fig_[system_type]_[description]`
- **Mathematical concepts**: `fig_[concept_name]`
- **Examples**: `fig_[example_name]`

### PGFPlots Conventions
- Use `myaxes` style for standard plots
- Use `myplotstyle` for specific signal plots
- **Continuous-time signals**: Use `domain` and `samples` for smooth curves
- **Discrete-time signals**: Use `ycomb` plots with `mark=*`
- **Colors**: Blue for primary, red for secondary, consistent color scheme
- **Grid**: Major and minor grids with appropriate styling

## Figure File Organization

### Directory Structure
```
figures/
├── lec01/
│   ├── fig_gaussian_pulse.tex
│   └── fig_sampled_gaussian.tex
├── lec02/
│   ├── fig_ct_exponentials.tex
│   ├── fig_dt_exponentials.tex
│   └── ...
└── lecXX/
    └── fig_[name].tex
```

### Figure File Naming
- Use descriptive names that indicate content
- Prefix with `fig_` for all figure files
- Use underscores to separate words
- Be consistent with signal type prefixes (`ct_`, `dt_`)

## Mathematical Content Standards

### Equation Formatting
- Use `\[ \]` for display equations
- Use `\( \)` for inline math
- Align equations using `align` environment when appropriate
- Number important equations with `\tag{}`

### Proof Formatting
```latex
\begin{proof}
	[Proof steps]
\end{proof}
```

### Mathematical Environments
- Use `definition` for new terms
- Use `proposition` for intermediate results
- Use `theorem` for major results
- Use `example` for worked examples
- Use `remark` for important observations

## Summary Section Format

### Standard Summary Structure
```latex
\section*{Summary and Next Lecture}
	\begin{itemize}[noitemsep]
		\item [Key takeaway 1]
		\item [Key takeaway 2]
		\item [Key takeaway 3]
		\item [Key takeaway 4]
		\item \textbf{Next time:} [Next lecture preview]
	\end{itemize}
```

## Cross-References and Labels

### Labeling Convention
- **Figures**: `fig:[descriptive_name]`
- **Sections**: `sec:[section_name]`
- **Equations**: `eq:[equation_name]`
- **Theorems**: `thm:[theorem_name]`

### Reference Format
- Use `\ref{fig:label}` for figure references
- Use `\ref{sec:label}` for section references
- Use `\ref{eq:label}` for equation references

## Consistency Guidelines

### Spacing
- Use `\vspace{0.4cm}` after title block
- Use `\vspace{0.2cm}` for small spacing adjustments
- Use `\hrule` for horizontal rules
- Use `\hrulefill` for horizontal fill

### Typography
- Use `\textbf{}` for bold text
- Use `\textit{}` for italic text
- Use `\Large` for large text
- Use `\small` for small text

### Mathematical Typesetting
- Use `\mathbb{}` for number sets
- Use `\mathcal{}` for operators
- Use `\mathrm{}` for differential operators
- Use `\text{}` for text in math mode

## File Maintenance

### Version Control
- Keep backup copies of working files
- Use descriptive commit messages
- Tag major versions

### Quality Assurance
- Check for consistent formatting
- Verify all cross-references work
- Ensure figure files exist and compile
- Test compilation before finalizing

## Best Practices

1. **Consistency**: Follow established patterns exactly
2. **Clarity**: Use clear, descriptive names and captions
3. **Completeness**: Include all necessary information
4. **Accuracy**: Verify mathematical content and references
5. **Maintainability**: Use consistent structure for easy updates

This template and conventions document should be used as the standard for all future lecture development to ensure consistency across the entire Signals and Systems course series.
