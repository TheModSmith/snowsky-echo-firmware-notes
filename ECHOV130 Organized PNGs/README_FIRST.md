# Organized Echo PNG Assets

This package reorganizes the extracted Echo `ROCK26IMAGERES` PNG files for manual review.

## Included

- `00_all_images_indexed/` — all 817 real PNG entries in index order.
- `01_large_fullscreen_480x222/` — major full-screen/background candidates.
- `02_candidate_sequences/` — ranges that look like animations or related UI groups.
- `03_large_panels_and_strips/` — large partial-screen panels and strips grouped by size.
- `04_icons_sprites_small_ui/` — common icon/sprite dimensions.
- `05_by_dimension/` — images grouped by dimensions where available.
- `06_tiny_text_glyphlike_and_indicators/` — very small UI/text/glyph-like resources.
- `ASSET_INDEX.tsv` — complete index, dimensions, offsets, filenames.
- `DIMENSION_SUMMARY.tsv` — counts by image size.
- `GALLERY.html` — browser gallery for quick visual review.

- PNGs are decoded as `bgr565_be`.
- The set contains 817 unique indexed images.
- Some images are duplicated into multiple folders to make manual review easier.
