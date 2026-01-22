# Mask Unfolder - Project Context for Claude Code

## Project Overview
This is a web application that converts folded mask designs into print-ready unfolded patterns for manufacturers. It solves the accordion fold geometry problem for pleated face masks.

## The Problem We're Solving
Pleated face masks use accordion folds to compress vertically. When designing a pattern:
- What you want to see when FOLDED must be split across UNFOLDED sections
- Some sections get hidden (tucked into folds)
- The pattern must be pre-distorted to look correct when folded

## The Geometry

### Fold Pattern
- **Total rows when unfolded**: 7 rows
- **Visible rows when folded**: Rows 1, 2, 4, 6, 7 (5 sections)
- **Hidden rows (tucked in folds)**: Rows 3, 5 (2 sections)

### How It Works
1. User uploads desired FOLDED appearance (e.g., 500×250px)
2. App creates UNFOLDED version (e.g., 542px tall for 500px wide)
3. Distributes folded image across 7 rows:
   - Row 1: Top of folded image (visible section 0)
   - Row 2: Second visible section (visible section 1)  
   - Row 3: **MIRROR of row 2** (hidden - folds under)
   - Row 4: Third visible section (visible section 2)
   - Row 5: **MIRROR of row 4** (hidden - folds under)
   - Row 6: Fourth visible section (visible section 3)
   - Row 7: Bottom visible section (visible section 4)
4. Outputs 300 DPI print-ready file (2066×2244px for 175mm×190mm)

### Why Mirroring?
When the mask folds, rows 3 and 5 fold backwards (accordion Z-shape). Mirroring ensures the pattern looks continuous even though those sections face the opposite direction.

## Technical Implementation

### Core Algorithm (in `generateUnfolded()`)
```javascript
// Constants
const totalRows = 7;
const visibleRows = [0, 1, 3, 5, 6]; // indices for rows 1,2,4,6,7
const hiddenRows = [2, 4]; // indices for rows 3,5

// Calculate dimensions
const unfoldedHeight = inputWidth * 190 / 175; // 175:190 aspect ratio
const rowHeight = unfoldedHeight / totalRows;
const visibleSectionHeight = inputHeight / visibleRows.length;

// For each row:
for (let rowIdx = 0; rowIdx < totalRows; rowIdx++) {
    if (visibleRows.includes(rowIdx)) {
        // Draw from input image
        const visibleIdx = visibleRows.indexOf(rowIdx);
        const sourceY = visibleIdx * visibleSectionHeight;
        // Draw section to canvas
    } else {
        // Mirror the row above
        const mirrorSourceY = (rowIdx - 1) * rowHeight;
        // Get row above, flip vertically, paste
    }
}
```

### Key Functions
- `loadImage(file)`: Loads user's image, displays preview
- `generateUnfolded()`: Core transformation logic
- `downloadBtn`: Scales to 300 DPI (2066×2244px)

## File Structure
```
mask-unfolder/
├── index.html          # Main app (rename mask-unfolder.html)
├── README.md           # User documentation
├── CONTEXT.md          # This file - for Claude Code
├── package.json        # If using Node.js deployment
└── server.js           # If using Node.js deployment
```

## Physical Dimensions
- **Unfolded mask**: 175mm wide × 190mm tall
- **Folded mask**: 175mm wide × ~65mm tall (when pleated)
- **Print resolution**: 300 DPI
- **Pixel dimensions**: 2066 × 2244 pixels

## Vendor Specifications
Based on actual mask manufacturer specs:
- Material printed flat
- Two horizontal accordion pleats
- Pleats occur after rows 2 and 4 (hiding rows 3 and 5)
- Ear loop attachment areas at sides (not covered by pattern)

## Design Decisions

### Why Canvas API?
- Client-side processing (no server needed)
- Direct pixel manipulation for mirroring
- Image scaling for 300 DPI output
- Works in all modern browsers

### Why No Dependencies?
- Pure HTML/CSS/JS keeps deployment simple
- No build process needed
- Works immediately on GitHub Pages/Netlify
- Small file size (~15KB)

### Styling Choices
- Cyberpunk/technical aesthetic
- Monospace fonts (JetBrains Mono, Space Mono)
- Dark theme with green accents (#00ff88)
- Grid texture background
- Reflects the technical/experimental nature of adversarial masks

## Testing Checklist
When modifying the app:
- [ ] Upload various image sizes (small, large, wide, tall)
- [ ] Verify row mirroring (rows 3 and 5 should flip)
- [ ] Check 300 DPI output dimensions (2066×2244)
- [ ] Test drag-and-drop vs click-to-upload
- [ ] Verify preview displays correctly
- [ ] Test download filename generation
- [ ] Check responsive layout on mobile

## Common Issues & Solutions

### Issue: Output looks wrong when folded
- **Check**: Row indices in visibleRows array
- **Solution**: Ensure [0,1,3,5,6] matches visible sections

### Issue: Mirrored sections don't align
- **Check**: rowHeight calculation consistency
- **Solution**: Use Math.floor() for pixel-perfect alignment

### Issue: 300 DPI file is wrong size
- **Check**: pixelsPerMM calculation (300/25.4)
- **Solution**: Should be 2066×2244 for 175×190mm

## Future Enhancement Ideas
- [ ] Batch processing multiple images
- [ ] Preview of folded result (simulate accordion)
- [ ] Custom dimension input (other mask sizes)
- [ ] Save/load presets
- [ ] Add grid overlay to show fold lines
- [ ] Export fold instructions PDF
- [ ] Integration with mask vendor APIs

## Related Research
This app was built based on the adversarial mask paper:
- **Paper**: "Adversarial Mask: Real-World Universal Adversarial Attack on Face Recognition Models"
- **ArXiv**: 2111.10759
- **Authors**: Zolfi, Avidan, Elovici, Shabtai
- **GitHub**: github.com/AlonZolfi/AdversarialMask

The accordion fold geometry was reverse-engineered from actual mask manufacturer specifications and sample images.

## Development History
Key learnings during development:
1. Initially thought pleats compressed image (wrong!)
2. Realized pleats HIDE sections (correct!)
3. Discovered mirroring needed for hidden sections
4. Found correct visible row pattern: 1,2,4,6,7 (not alternating)
5. Determined proper aspect ratio: 175:190 (not square)

## For Claude Code Agent
When working on this project:
- The geometry is finalized and tested with real manufacturer
- Core algorithm in `generateUnfolded()` is production-ready
- Focus enhancements on UX, features, or documentation
- Test any geometry changes with sample images
- Preserve the 7-row, 5-visible, 2-hidden pattern
- Maintain 175mm×190mm output dimensions

## Quick Reference: Row Mapping
```
INPUT (Folded):    OUTPUT (Unfolded):
Section 0     →    Row 1 (visible)
Section 1     →    Row 2 (visible)
                   Row 3 (hidden - mirror of row 2)
Section 2     →    Row 4 (visible)
                   Row 5 (hidden - mirror of row 4)
Section 3     →    Row 6 (visible)
Section 4     →    Row 7 (visible)
```

## Contact & Support
This app was developed through iterative collaboration between a human expert in adversarial ML and Claude (Anthropic's AI assistant). The geometry was validated with actual mask manufacturer samples.

For questions about:
- **Geometry**: Refer to fold pattern section above
- **Code**: See inline comments in index.html
- **Deployment**: See README.md
- **Adversarial masks**: See ArXiv paper 2111.10759
