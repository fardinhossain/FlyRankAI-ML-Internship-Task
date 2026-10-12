# IEEE Conference LaTeX Research Paper — FlyRank ML Internship (ML-11)

This directory contains the complete, publication-ready research paper prepared using the official **IEEE Conference LaTeX format** (`\documentclass[conference]{IEEEtran}`).

## Project Structure

```text
paper/
├── main.tex              # Full IEEE conference paper manuscript
├── references.bib        # Verified BibTeX bibliography (IEEEtran format)
├── figures/              # High-resolution PNG figures from empirical experiments
│   ├── cost_value_matrix.png
│   ├── action_mix.png
│   ├── confidence_mix.png
│   └── top_reason_codes.png
└── README.md             # Compilation and Overleaf import instructions
```

---

## How to Review and Compile on Overleaf

You can review, edit, and compile this manuscript on [Overleaf](https://www.overleaf.com/) in under two minutes:

### Option 1: Direct Zip Upload (Fastest)
1. Compress the entire `paper/` folder into a `.zip` archive (containing `main.tex`, `references.bib`, and the `figures/` folder).
2. Go to **[Overleaf](https://www.overleaf.com/)** and log in.
3. Click **New Project** $\rightarrow$ **Upload Project**.
4. Drag and drop the `.zip` file.
5. Overleaf will automatically detect `main.tex` and compile the two-column IEEE PDF.

### Option 2: Using the Official IEEE Overleaf Template
1. Open the [Official IEEE Conference Template on Overleaf](https://www.overleaf.com/latex/templates/ieee-conference-template/grfzhhncsfqn).
2. Click **Open as Template**.
3. Replace the template's `main.tex` with the contents of [`paper/main.tex`](main.tex).
4. Upload [`paper/references.bib`](references.bib) and the `figures/` folder into the Overleaf file tree.
5. Click **Recompile** (`Ctrl + Enter`).

---

## Local Compilation (LaTeX / TeX Live / MiKTeX)

If you have a local TeX distribution installed:

```bash
cd paper
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

This generates `main.pdf` with properly numbered sections, resolved citations, cross-referenced tables, and embedded high-resolution figures.

---

## Public Deployment & Web Artifacts

The research paper is also deployed as a publicly accessible, responsive research website on GitHub Pages:

- **Live Research Website:** [https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/](https://fardinhossain.github.io/FlyRankAI-ML-Internship-Task/)
- **One-Line Submission Receipt:** [`submission/paper_url.txt`](../submission/paper_url.txt)
- **Executable Capstone Notebook:** [`work/notebooks/capstone.ipynb`](../work/notebooks/capstone.ipynb)
- **GitHub Repository:** [https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task](https://github.com/fardinhossain/FlyRankAI-ML-Internship-Task)

---

## IEEE Compliance & Quality Checklist

- [x] Standard `\documentclass[conference]{IEEEtran}` document class
- [x] Exactly five complete sentences in the abstract
- [x] 4–6 relevant IEEE keywords in `IEEEkeywords`
- [x] Numbered IEEE sections I through X with clean mathematical equations
- [x] Unseen client holdout evaluation table ($N=6,163$, 0 client overlap)
- [x] Embedded experimental figures with descriptive captions
- [x] Mandatory data credit: *"Built on the FlyRank ML Internship dataset"* linking to [https://flyrank.ai/](https://flyrank.ai/)
- [x] Verified IEEEtran BibTeX citations without fabricated sources
- [x] 100% public-safe: no confidential client names, internal URLs, or private search queries
