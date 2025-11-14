# Signals and Systems Lecture Series

A comprehensive LaTeX-based lecture series covering Signals and Systems topics, including Fourier Series, Fourier Transform, Discrete-Time Fourier Transform, and related concepts.

## Overview

This folder contains the LaTeX source files for the Signals and Systems lecture series. All lectures are written in LaTeX with TikZ/PGFPlots figures for high-quality mathematical typesetting and visualizations.

## Structure

```
lectures/
├── signals-preamble.tex      # Shared LaTeX preamble with packages and macros
├── lecture_template.tex      # Template for creating new lectures
├── LECTURE_CONVENTIONS.md    # Style guide and conventions
├── README.md                 # This file
├── lec01.tex                 # Lecture 1: Introduction to Signals
├── lec02.tex                 # Lecture 2: Elementary Signals and Signal Properties
├── lec03.tex                 # Lecture 3: Systems and Their Properties
├── lec04.tex                 # Lecture 4: Convolution and LTI Systems
├── lec05.tex                 # Lecture 5: Convolution Examples and Properties
├── lec06.tex                 # Lecture 6: System Implementation and Properties
├── lec07.tex                 # Lecture 7: Fourier Series Introduction
├── lec08.tex                 # Lecture 8: Fourier Series Analysis
├── lec09.tex                 # Lecture 9: Fourier Series Applications
├── lec10.tex                 # Lecture 10: Fourier Transform Introduction
├── lec11.tex                 # Lecture 11: The Continuous-Time Fourier Transform (CTFT)
├── lec12.tex                 # Lecture 12: Properties of the Continuous-Time Fourier Transform
├── lec13.tex                 # Lecture 13: Convolution and Multiplication Properties
├── lec14.tex                 # Lecture 14: The Discrete-Time Fourier Transform (DTFT)
├── lec15.tex                 # Lecture 15: Properties of the Discrete-Time Fourier Transform
├── lec16.tex                 # Lecture 16: Duality and Time-Frequency Relationships
├── lec17.tex                 # Lecture 17: Magnitude and Phase Representation
├── lec18.tex                 # Lecture 18: Linear Phase Systems and Group Delay
├── lec19.tex                 # Lecture 19: Ideal vs. Non-Ideal Filters & Time-Domain Behavior
└── figures/                  # All figure source files organized by lecture
    ├── lec01/
    ├── lec02/
    └── ...
```

## Prerequisites

To compile these LaTeX documents, you need:

- **LaTeX Distribution**: TeX Live (recommended) or MiKTeX
  - **TeX Live**: [https://www.tug.org/texlive/](https://www.tug.org/texlive/)
  - **MiKTeX**: [https://miktex.org/](https://miktex.org/)

- **Required LaTeX Packages** (included in `signals-preamble.tex`):
  - `amsmath`, `amssymb`, `mathtools` - Mathematical typesetting
  - `geometry` - Page layout
  - `enumitem` - List formatting
  - `xcolor` - Colors
  - `microtype` - Typography improvements
  - `graphicx` - Graphics support
  - `tikz`, `pgfplots` - Diagrams and plots
  - `subcaption` - Subfigures
  - `amsthm` - Theorem environments
  - `hyperref` - Hyperlinks
  - `array` - Array/tabular extensions

## Compiling Lectures

### Compile a Single Lecture

Navigate to the `lectures/` directory and run:

```bash
cd lectures
pdflatex lec11.tex
pdflatex lec11.tex  # Run twice for cross-references
```

Or using a build tool:

```bash
cd lectures
latexmk -pdf lec11.tex
```

### Compile All Lectures

**On Linux/macOS:**
```bash
cd lectures
for file in lec*.tex; do
    pdflatex "$file"
    pdflatex "$file"
done
```

**On Windows (PowerShell):**
```powershell
cd lectures
Get-ChildItem -Filter "lec*.tex" | ForEach-Object {
    pdflatex $_.Name
    pdflatex $_.Name
}
```

**Using latexmk (recommended):**
```bash
cd lectures
latexmk -pdf lec*.tex
```

### Build Artifacts

The compilation process generates several auxiliary files (`.aux`, `.log`, `.out`, `.synctex.gz`). These are automatically ignored by Git (see `.gitignore` in the repository root). To clean them:

**On Linux/macOS:**
```bash
cd lectures
rm -f *.aux *.log *.out *.synctex.gz
```

**On Windows (PowerShell):**
```powershell
cd lectures
Remove-Item *.aux,*.log,*.out,*.synctex.gz -ErrorAction SilentlyContinue
```

## Content Overview

### Core Topics Covered

1. **Signals and Systems Fundamentals** (Lectures 1-3)
   - Signal definitions and classifications
   - Elementary signals (impulse, step, exponentials)
   - System properties (linearity, time-invariance, causality, stability)

2. **Convolution and LTI Systems** (Lectures 4-6)
   - Impulse response
   - Convolution integral and sum
   - System implementation structures

3. **Fourier Series** (Lectures 7-9)
   - Periodic signal representation
   - Fourier series coefficients
   - Applications and properties

4. **Continuous-Time Fourier Transform** (Lectures 10-13)
   - CTFT definition and properties
   - Convolution and multiplication properties
   - Applications

5. **Discrete-Time Fourier Transform** (Lectures 14-15)
   - DTFT definition and properties
   - Periodicity and convergence

6. **Advanced Topics** (Lectures 16-19)
   - Duality relationships
   - Magnitude and phase representation
   - Linear phase systems and group delay
   - Ideal vs. non-ideal filters

## Style and Conventions

All lectures follow consistent formatting and style guidelines documented in `LECTURE_CONVENTIONS.md`. Key conventions include:

- **Mathematical Notation**: Standard signals and systems notation
- **Figure Naming**: Descriptive names with `fig_` prefix
- **Section Structure**: Consistent organization across all lectures
- **Theorem Environments**: Custom theorem styles for definitions, examples, etc.

## Creating New Lectures

1. Copy `lecture_template.tex` to create a new lecture file
2. Update the lecture number, title, and content
3. Create figure files in the appropriate `figures/lecXX/` directory
4. Follow the conventions in `LECTURE_CONVENTIONS.md`

## Contributing

If you find errors or have suggestions for improvements:

1. **Report Issues**: Open an issue on the repository
2. **Suggest Improvements**: Propose enhancements via issues or pull requests
3. **Fix Errors**: Submit pull requests with corrections

### Contribution Guidelines

- Maintain consistency with existing style and conventions
- Ensure all LaTeX files compile without errors
- Update cross-references when adding new content
- Test compilation before submitting changes

## Authors

- **Dr. Ghandi Manasra**
- **Ahmed Rabei**

## References

Primary textbook reference:
- Oppenheim & Willsky, *Signals and Systems*, 2nd Edition

## Related Resources

- [LaTeX Project](https://www.latex-project.org/)
- [TikZ & PGF Manual](https://tikz.dev/)
- [PGFPlots Manual](http://pgfplots.sourceforge.net/)

---

**Note**: This folder contains LaTeX source files. To view the lectures, compile them to PDF using a LaTeX distribution. For repository setup instructions, see the `GITHUB_SETUP_GUIDE.md` in the repository root.

