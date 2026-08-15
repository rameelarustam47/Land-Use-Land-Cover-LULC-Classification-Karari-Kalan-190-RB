
## Overview

This project maps land cover for **Chak No. 190 RB, Karari Kalan**, a village in Faisalabad District, Punjab. It classifies the area into 10 land cover types using a supervised CART classifier trained on manually digitized ground-truth points, then validates results with a confusion matrix and Kappa statistic.

## Data Sources (all free and open)

| Layer | Source | Resolution |
|---|---|---|
| Satellite imagery | Sentinel-2 SR Harmonized (`COPERNICUS/S2_SR_HARMONIZED`) | 10 m |
| Cloud masking | Google Cloud Score+ (`GOOGLE/CLOUD_SCORE_PLUS/V1/S2_HARMONIZED`) | 10 m |
| Village boundary | Manually digitized in GEE, uploaded as a GEE asset | — |

## Classes

1. Residential
2. Agriculture
3. Bypass (road)
4. Factory
5. Graveyard
6. Drainwater
7. School
8. Klin (brick kiln)
9. Water Tank
10. Pond

## Method

1. Build a cloud-free Sentinel-2 composite (Jan 2025 – Aug 2026) using Cloud Score+ masking.
2. Digitize training points for each land cover class directly on the composite.
3. Sample image bands (B2, B3, B4, B8) at each training point.
4. Split samples 70/30 into training and test sets.
5. Train a CART classifier and classify the full image.
6. Validate with a confusion matrix, Overall Accuracy, and Kappa coefficient.
7. Calculate area per class and export the classified raster.

## Results

- **Overall Accuracy:** ~93–95%
- **Kappa:** ~0.78–0.85 (good to excellent agreement)
- Strongest classes: Agriculture, Residential, Factory
- Weakest classes: Bypass, Drainwater (small sample sizes, spectral overlap with built-up/bare surfaces)


## Limitations

- Sentinel-2's 10 m resolution limits detection of very small features (single water tanks, narrow drains).
- Classes with few training points (Klin, Pond, Water Tank) have lower statistical reliability despite good visual accuracy.
- Cloud cover during monsoon months can reduce the number of usable clear-sky scenes.



## Author

Your name here — internship/university project, 2026.
