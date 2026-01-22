# Mask Unfolder

Convert folded mask designs into print-ready unfolded patterns. Solves the accordion fold geometry problem for pleated face masks.

## The Problem

Pleated face masks use accordion folds to compress vertically. When you design a pattern for printing:

- What you see when the mask is **folded** must be split across multiple sections when **unfolded**
- Some sections get hidden inside the folds
- The pattern must be pre-distorted to look correct when folded

This app automatically handles that transformation.

## How to Use

1. **Upload your design** - The image of what you want to appear on the folded mask (recommended: 500×250px)
2. **Preview** - See how it will be split across the unfolded pattern
3. **Download** - Get a print-ready 300 DPI file (2066×2244px) for manufacturers

The output is sized for standard pleated masks: **175mm wide × 190mm tall** when unfolded.

## The Geometry

The app distributes your design across **7 rows**:

| Row | Type | Source |
|-----|------|--------|
| Row 1 | Visible | Top of your design (section 0) |
| Row 2 | Visible | Second section (section 1) |
| Row 3 | Hidden | **Mirrored copy of row 2** |
| Row 4 | Visible | Third section (section 2) |
| Row 5 | Hidden | **Mirrored copy of row 4** |
| Row 6 | Visible | Fourth section (section 3) |
| Row 7 | Visible | Bottom section (section 4) |

### Why Mirroring?

When the mask folds accordion-style, rows 3 and 5 fold backwards (creating a Z-shape). Mirroring these sections ensures the pattern looks continuous even though they face the opposite direction.

### The Fold Pattern

- **Unfolded**: 7 rows total, 175mm × 190mm
- **Folded**: 5 visible sections, 175mm × ~65mm
- **Hidden rows**: Rows 3 and 5 (tucked into the accordion pleats)
- **Pleats occur**: Between rows 2-3 and rows 4-5

## For Manufacturers

The downloaded file is ready to print on flat mask material at 300 DPI. When accordion-folded with pleats in the specified locations, the original design will appear correctly on the folded mask.

Standard mask specs:
- Material: Printed flat, then pleated
- Two horizontal accordion pleats
- Ear loop attachment areas at sides (not affected by pattern)

## Technical Details

- **Pure HTML/CSS/JavaScript** - Works entirely in your browser, no server needed
- **Canvas API** - Client-side image processing and manipulation
- **No build step** - Single HTML file with embedded styles and scripts
- **Privacy-first** - Your images never leave your device

## Related Research

This app is based on the accordion fold geometry from adversarial mask research:

- **Paper**: "Adversarial Mask: Real-World Universal Adversarial Attack on Face Recognition Models"
- **ArXiv**: [2111.10759](https://arxiv.org/abs/2111.10759)
- **Authors**: Zolfi, Avidan, Elovici, Shabtai
- **GitHub**: [AlonZolfi/AdversarialMask](https://github.com/AlonZolfi/AdversarialMask)

The fold pattern was reverse-engineered from actual mask manufacturer specifications.
