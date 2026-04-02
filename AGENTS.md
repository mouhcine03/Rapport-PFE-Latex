# AGENTS.md - AI Agent Guidelines for PFE LaTeX Report

## Project Overview
This is a LaTeX-based **PFE (Projet de Fin d'Études / End-of-Studies Project)** report for an engineering degree at **ENSA Kénitra** (Université Ibn Tofail, Morocco).

**Topic:** Implementation of an integration solution between **Boomi** and **Infor** to automate work order management.

**Student:** Mouhcine EL HASNAOUI  
**Host Company:** We are beebay  
**Defense Date:** 07/02/2024

---

## Project Structure

```
Repport-PFE-Latex/
├── main.tex                 # Main LaTeX document (entry point)
├── front/
│   └── page_garde.tex       # Cover page with university logos, jury info
├── chapters/
│   ├── Dedicace.tex         # Dedication page
│   ├── Remerciements.tex    # Acknowledgments
│   ├── Abstract.tex         # English abstract
│   ├── Resume.tex           # French résumé
│   ├── introduction.tex     # Project introduction (placeholder)
│   └── conclusion.tex       # Project conclusion (placeholder)
├── images/
│   ├── Ensa-logo.png        # ENSA university logo
│   └── beebaydigital_logo.jpg # Company logo
└── .gitignore               # LaTeX build artifacts
```

---

## Build & Validation Commands

### Build Commands
```bash
# Single build (may need 2-3 runs for references)
pdflatex main.tex

# Recommended: automatic rebuilds until stable
latexmk -pdf main.tex

# Clean build artifacts
latexmk -c main.tex

# Full clean (removes .pdf too)
latexmk -C main.tex
```

### Linting & Validation
```bash
# Syntax checking (if chktex installed)
chktex main.tex

# Check for undefined references in log
grep -i "undefined reference" main.log

# Check for missing images
grep -i "file not found" main.log
```

### Quick Validation Workflow
1. Run `pdflatex main.tex` twice
2. Check `main.log` for errors (not warnings)
3. Verify PDF renders correctly
4. Confirm all references resolve (no "??")

---

## LaTeX Code Style Guidelines

### File Organization
- One chapter per `.tex` file in `chapters/`
- Front matter in `front/`
- Images in `images/` (referenced by filename only)
- Main document structure in `main.tex` only

### Imports & Packages
- All packages declared in `main.tex` preamble
- Standard packages: `graphicx`, `geometry`, `hyperref`, `tikz`, `xcolor`
- Language: `\usepackage[french]{babel}` with `T1` fontenc
- Add new packages to `main.tex`, not individual chapters

### Formatting Conventions
- 2-space indentation for nested environments
- Blank line before/after environments (`figure`, `table`, `center`)
- One sentence per line for easier diff tracking
- Use `\chapter{}` for numbered, `\chapter*{}` + `\addcontentsline{toc}{chapter}{...}` for unnumbered

### Naming Conventions
- Chapter files: `chapters/Name.tex` (PascalCase, French titles)
- Images: descriptive names with hyphens (`work-order-flow.png`)
- Labels: `fig:description`, `tab:description`, `sec:description`, `cha:description`
- Colors: camelCase (`primaryColor`, `secondaryColor`)

### Figures & Tables
```latex
\begin{figure}[h]
  \centering
  \includegraphics[width=0.7\textwidth]{image-name}
  \caption{Description en français}
  \label{fig:description}
\end{figure}
```

### Error Handling
- Use `\usepackage{graphicx}` before `\includegraphics`
- Wrap custom colors in `\definecolor` before use
- Use `\newgeometry`/`\restoregeometry` pairs for layout changes
- Check compilation log after each significant change

### Language Rules
- Main content: French (academic style)
- Abstract: English
- Use `\textit{}` for foreign terms (e.g., work orders)
- Preserve French typography (spaces before `:`, `;`, `!`, `?`)

---

## Common Tasks

### Add New Chapter
1. Create `chapters/new-chapter.tex`
2. Add `\include{chapters/new-chapter}` to `main.tex` (before conclusion)
3. Build twice to update references

### Add Image
1. Place in `images/` directory
2. Reference: `\includegraphics[width=0.7\textwidth]{filename.png}`

### Modify Cover Page
Edit `front/page_garde.tex` - uses TikZ for blue sidebar (`#003366`) and orange accent (`#FF9900`)

---

## Key Context
- **Jury:** M. NOUH Said (President), Mme RASSAA Oumaima (Sponsor), M. BAHASSINE Said (Examiner)
- **Department:** Intelligence Artificielle et Génie Informatique
- **Keywords:** Boomi, Infor, System Integration, Automation, Work Orders, Data Synchronization, iPaaS
- **Build artifacts:** Auto-generated files in `.gitignore` - never commit
