# LaTeX Submission for Assignment 1

## Files Included
- `STUDENTID_Assignment1_CS4203Fall2025.tex` - Main LaTeX document
- `README.md` - This file

## Required Images
The LaTeX document references diagram images from the `../Figures/` directory:
- `BlockDiagram.png`
- `UseCaseDiagram.png`
- `ClassDiagram.png`
- `ActivityDiagram.png`

Make sure these files exist in the `Figures` folder before compiling.

## Before Compiling
**IMPORTANT:** Replace `[INSERT YOUR STUDENT ID]` in the LaTeX file with your actual student ID.

## How to Compile

### Option 1: Using Overleaf (Recommended for beginners)
1. Go to [overleaf.com](https://www.overleaf.com)
2. Create a new blank project
3. Upload the `.tex` file
4. Create a `Figures` folder in Overleaf
5. Upload all four diagram images to the Figures folder
6. Click "Recompile" to generate the PDF

### Option 2: Using Local LaTeX Installation
If you have LaTeX installed on your computer:

```bash
cd LaTeX
pdflatex STUDENTID_Assignment1_CS4203Fall2025.tex
pdflatex STUDENTID_Assignment1_CS4203Fall2025.tex
```

(Run twice to generate the table of contents correctly)

### Option 3: Using VSCode with LaTeX Workshop
1. Install the "LaTeX Workshop" extension in VSCode
2. Open the `.tex` file
3. Press `Ctrl+Alt+B` (or Cmd+Option+B on Mac) to build
4. The PDF will be generated automatically

## Output
The compilation will generate:
- `STUDENTID_Assignment1_CS4203Fall2025.pdf` - Your submission file

## Troubleshooting

**Problem:** Images not showing
- **Solution:** Make sure the `Figures` folder is one level up from the LaTeX folder, or adjust the paths in the `.tex` file

**Problem:** "File not found" errors
- **Solution:** Check that all diagram images have the exact names referenced in the `.tex` file

**Problem:** Table of contents not showing
- **Solution:** Run pdflatex twice (first run generates ToC, second run includes it)

## What's Included in the PDF
- Title page with student ID
- Table of contents
- Part A: System Architecture Breakdown with block diagram
- Part B: Design Pattern summaries (Controller and Expert)
- Part C: All three UML diagrams (Use Case, Class, Activity) with explanations
- Part D: Pattern application reflection
- References

## Notes
- The PDF is formatted for professional submission
- All ASCII diagrams and construction instructions have been removed
- Only the final answers and actual diagrams are included
- Page numbers and headers are automatically generated

