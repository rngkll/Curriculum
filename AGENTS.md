# AGENTS.md - LaTeX CV/Resume Project Guidelines

This document provides guidelines for coding agents working on this LaTeX-based CV/Resume project.

## Project Overview

This is a personal CV project using the Friggeri LaTeX template with automated builds via CI/CD. The project generates a professional PDF resume from LaTeX source files.

**Technology Stack:**
- LaTeX with XeLaTeX/Tectonic engine
- Docker for containerized builds
- GitHub Actions for CI/CD automation
- Git for version control

## Build Commands

### Local Development

**Primary build command:**
```bash
docker run --mount src=$(pwd)/src,target=/usr/src/tex,type=bind dxjoke/tectonic-docker /bin/sh -c "tectonic cv.tex"
```

**Alternative build methods:**
```bash
# Using GitHub Actions setup locally (if tectonic installed)
cd src/
tectonic cv.tex

# For XeLaTeX (traditional method)
cd src/
xelatex cv.tex
biber cv
xelatex cv.tex
```

### CI/CD

**GitHub Actions:** Comprehensive build and release automation via `.github/workflows/tectonic.yml`
- **Pre-releases:** Created automatically on every main branch push
- **Official releases:** Created when pushing version tags (v*)
- **Enhanced features:** PDF validation, metadata generation, artifact management

### Testing

**No formal test suite** - validation occurs through successful compilation:
- Local: Run build command and verify PDF generation
- CI: GitHub Actions must pass without errors
- Manual: Review generated PDF for formatting and content accuracy

**GitHub Actions Workflow Testing:**
- **Feature branches:** Push to test workflow without creating releases
- **Main branch:** Triggers pre-release creation automatically
- **Version tags:** Creates official releases (use format: v1.4, v1.5, etc.)
- **Artifacts:** All builds generate PDF artifacts retained for 30 days

### Single File Testing

To test changes to a specific LaTeX file:
```bash
# Test main CV
docker run --mount src=$(pwd)/src,target=/usr/src/tex,type=bind dxjoke/tectonic-docker /bin/sh -c "tectonic cv.tex"
```

## Code Style Guidelines

### LaTeX Formatting

**File Structure:**
- Use clear section headers with comments (`%----------------------------------------------------------------------------------------`)
- Maintain consistent indentation (2-4 spaces per level)
- Group related content with blank lines
- Keep line length reasonable (~80-100 characters)

**Document Classes:**
- Main CV uses `\documentclass[]{friggeri-cv}`
- Custom class modifications in `friggeri-cv.cls` and `cv-friggeri-x.cls`
- Use semantic markup over direct formatting

**Content Organization:**
```latex
% Good - semantic structure
\section{experience}
\begin{entrylist}
\entry
{2019--Now}
{Company Name}
{Location}
{\emph{Job Title} \\
Description of responsibilities...}
\end{entrylist}

% Avoid - direct formatting without structure
{\bf 2019--Now} Company Name, Location
Job Title
Description...
```

### Bibliography (BibTeX)

**Entry formatting:**
- Use consistent field naming
- Include DOI and URL when available
- Maintain alphabetical order by entry key
- Use descriptive entry keys (author:year:venue format)

**Example:**
```bibtex
@article{segura:2024:ieee:1,
  AUTHOR = {Segura, Alvaro and Smith, John},
  TITLE = {{Title of the Paper}},
  JOURNAL = {{IEEE Transactions on Something}},
  VOLUME = {42},
  PAGES = {1--10},
  YEAR = {2024},
  DOI = {10.1109/example.2024.1234567}
}
```

### File Naming

**Conventions:**
- Main files: `cv.tex`, `bibliography.bib`
- Class files: `*.cls` (lowercase, hyphenated)
- Resources: descriptive names in `fonts/` or `resources/`
- Generated files: Follow LaTeX conventions (`.aux`, `.bbl`, `.log`, etc.)

### Git Ignore Patterns

**LaTeX-specific ignores:**
```
*.swp
*.swo
*.aux
*.bbl
*.blg
*.bcf
*.log
*.out
*.xml
```

## Error Handling

### Common LaTeX Errors

**Font issues:**
- Ensure custom fonts are in `fonts/` directory
- Verify font loading in class file
- Check XeLaTeX compatibility

**Bibliography errors:**
- Run biber after first LaTeX compilation
- Check `.bib` file syntax
- Verify citations match bibliography entries

**Docker issues:**
- Ensure Docker is running
- Check mount paths are correct
- Verify working directory is repository root

### Debugging Workflow

1. **Check compilation logs** in terminal output
2. **Examine generated `.log` file** in src directory
3. **Validate LaTeX syntax** using online validators
4. **Test with minimal example** to isolate issues
5. **Compare with working version** in git history

## Version Control

### Branch Strategy
- `main` branch for stable versions
- Feature branches for all changes via Pull Requests
- **NEVER commit directly to main** - always use PR workflow

### Commit Guidelines
- Focus commits on logical changes
- Include both source and generated PDF when relevant
- Clear commit messages describing the change purpose
- Don't commit LaTeX auxiliary files (use .gitignore)

### Release Process
- **Pre-releases:** Created automatically on every main branch push
- **Official releases:** Created when pushing version tags (v*)
- GitHub Actions provides continuous validation
- Manual verification of PDF output before tagging

## Directory Structure

```
/
├── src/                    # Main CV source directory
│   ├── cv.tex             # Primary CV document
│   ├── cv.pdf             # Compiled output
│   ├── friggeri-cv.cls    # LaTeX class file
│   ├── cv-friggeri-x.cls  # Modified class file
│   ├── bibliography.bib   # Bibliography/publications
│   └── fonts/             # Custom fonts (Lato, TeX Gyre Heros)
└── .github/workflows/     # CI/CD configuration
```

## Best Practices

1. **Always test locally** before pushing changes
2. **Use feature branches** and create Pull Requests for all changes
3. **Use semantic LaTeX markup** over direct formatting
4. **Keep bibliography updated** and properly formatted
5. **Verify PDF output** after any changes
6. **Follow existing code patterns** in the template
7. **Use Docker for consistent builds** across environments
8. **Check CI status** before considering changes complete

## Resources

- [Friggeri Resume Template](https://www.latextemplates.com/template/friggeri-resume-cv)
- [Tectonic LaTeX Engine](https://tectonic-typesetting.github.io/)
- [Docker Tectonic Image](https://hub.docker.com/r/dxjoke/tectonic-docker)
- [Setup Tectonic Action](https://github.com/WtfJoke/setup-tectonic)
