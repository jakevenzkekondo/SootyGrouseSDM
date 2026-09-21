# Sooty Grouse Species Distribution Model

This project is a species distribution model (SDM) predicting Sooty Grouse (*Dendragapus fuliginosus*) breeding and brood-rearing season habitat suitability across Oregon, implemented in a Jupyter notebook using Google Earth Engine and a Random Forest classifier. The model produces two outputs: a continuous **habitat suitability map** (mean predicted probability of occurrence across 10 spatial cross-validation folds, 0–1) and a binary **potential distribution map** (majority-vote predicted presence/absence across the same 10 folds). This model was developed as a passion project with the goal of supporting conservation efforts of the Sooty Grouse in the study area. 

Full methodology, results, and discussion are available in [`Sooty_Grouse_SDM_Report.pdf`](./Sooty_Grouse_SDM_Report.pdf).

## Overview

- **Species:** Sooty Grouse
- **Study area:** Oregon sub-section
- **Temporal scope:** Breeding and brood-rearing season (April–September)
- **Occurrence data:** [GBIF](https://www.gbif.org/) occurrence search API
- **Environmental predictors:** NASA SRTM elevation/terrain, USGS NLCD land cover, WorldClim climate variables
- **Model:** Random Forest (`ee.Classifier.smileRandomForest`), evaluated via spatial block cross-validation

This project follows the structure of Google Earth Engine's [community SDM tutorial](https://developers.google.com/earth-engine/tutorials/community/species-distribution-modeling/species-distribution-modeling), adapted for Sooty Grouse and Oregon's geographic scale.

## Repository structure

```
SootyGrouseSDM/
├── src/            # Main analysis notebook
├── figures/        # Exported plots (correlation matrix, variable importance, ROC curves, etc.)
├── maps/           # Exported spatial maps (predictors, study area, model outputs)
├── requirements.txt
├── .env.example
└── Report.pdf      # Full write-up (methods, results, discussion)
```

## Setup

1. Clone the repo and create a virtual environment:
   ```bash
   git clone https://github.com/jakevenzkekondo/SootyGrouseSDM.git
   cd SootyGrouseSDM
   python -m venv .venv
   source .venv/bin/activate  # or .venv\Scripts\activate on Windows
   pip install -r requirements.txt
   ```

2. Create a `.env` file and add your own Google Earth Engine project ID:
   ```
   GEE_PROJECT_ID=your-gee-project-id
   ```
   You can use .ev.example for reference.
   
   This project requires a [Google Earth Engine account](https://earthengine.google.com/) with a registered Cloud project.

3. Open `src/sdm.ipynb` and run cells sequentially. Earth Engine authentication will prompt on first run.

## Data sources and citations

Occurrence data for this project was retrieved via the GBIF occurrence search API:

> GBIF.org (2026). GBIF Home Page. Available at: https://www.gbif.org [Accessed 18 September 2026].

Environmental predictors:
- NASA SRTM Digital Elevation (`USGS/SRTMGL1_003`)
- USGS NLCD 2021 land cover (`USGS/NLCD_RELEASES/2021_REL/NLCD`)
- WorldClim BIO variables (`WORLDCLIM/V1/BIO`)

All environmental predictors accessed via [Google Earth Engine](https://earthengine.google.com/).

This project's workflow was adapted from:

> Google Earth Engine Developers (n.d.). *Species Distribution Modeling* [Community Tutorial]. Available at: https://developers.google.com/earth-engine/tutorials/community/species-distribution-modeling/species-distribution-modeling

## License

This project is licensed under the MIT License — see [LICENSE](./LICENSE) for details.
