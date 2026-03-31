# MASFI: Mapping Alternative Scenarios of Forest Intactness

A cloud-based machine learning framework for predicting actual and alternative aboveground biomass density (AGBD) at 30 m resolution. MASFI uses GEDI L4A footprints, XGBoost regression and features engineered from the JRC Tropical Moist Forest product to quantify forest disturbance, restoration potential and relative intactness with IPCC-compliant uncertainty estimates. Outputs support protected area delineation, monitoring and management. This framework informed the gazettement of the Al-Sultan Abdullah Royal Tiger Reserve in Pahang, Malaysia.

## Framework Components

- **1_areas**: Project area delineation and raster template creation from the Copernicus GLO-30 DEM, including pixel area calculation on the WGS84 ellipsoid.
- **2_targets**: GEDI L4A download via NASA CMR API, quality filtering, and extraction of AGBD with standard error and elevation. Also supports user data upload.
- **3_features_lcluc**: Download and engineering of scenario features from the TMF annual classification and disturbance products. Binary rasters are converted to edge distance and local density metrics within a 120 m ecological threshold. Old-growth proxy and forest reserve polygons are rasterised similarly.
- **3_features_topo**: Engineering of static topographic features from a Digital Terrain Model, including 24 metrics (slope, topographic position index, stream power index, etc.) in smoothed and unsmoothed variants. Geographic features (latitude, longitude, distance to coast) are also created here.
- **4_datasets**: Spatial and temporal matching of GEDI footprints with feature rasters.
- **5_models**: XGBoost hyperparameter optimisation using a custom SHAP-guided random search, cross-validation, and SHAP feature interpretation. Supports multi-runtime parallel optimisation.
- **6_scenarios**: Compilation of feature stacks for yearly, undisturbed, disturbance area and recovery scenarios. Scenario features are modified to simulate alternative states while static features remain unchanged.
- **7_predictions**: Predictions with multi-iteration Monte Carlo simulation propagating GEDI L4A standard error through model training to pixel-level 95% confidence intervals (IPCC Approach 2). Accuracy comparison with existing products.
- **8_differences**: Disturbance and restoration potential from scenario differences, with uncertainty propagation (IPCC Approach 1). Percentage loss and quantile-based relative intactness scoring on a 0–10 scale.
- **9_statistics**: Area-based aggregation of AGB, disturbance, restoration and intactness statistics by polygon, with Sankey diagrams and yearly trend plots.

## Requirements

- Familiarity with Python, Google Colab and Google Drive. The workflow is largely automated but requires editing of some variables for different use cases.
- Google Account with at least 20 GB Drive. 100 GB – 2 TB is more realistic for most project areas, depending on spatial extent. GEDI downloads take the majority of the space, and the total required will be indicated before downloads begin.
- A Colab subscription is not required but highly recommended for faster runtimes and more RAM to accommodate larger project areas. The Pro+ subscription also allows background processing.
- The project area should be within GEDI coverage (51.6°N to 51.6°S) and ideally the tropical moist forest biome. The framework can be adapted to other biomes using equivalent forest cover and disturbance products, though modifications to target filtering and scenario design would be needed.
- Old-growth or mature forest proxy polygons within or adjacent to the project area. Without these, the earliest available satellite baseline (e.g. 1990s) can be used, with the understanding that pre-satellite degradation will be invisible and restoration potential underestimated.

## Getting Started

1. Prepare a project area polygon as a .gpkg, along with any land-use polygons (old-growth protected areas, management units, etc.).
2. Download the notebooks and place in an empty Google Drive folder or Shared Drive.
3. Open the notebooks in Google Colab, starting with 1_areas, running code blocks sequentially.
4. Instructions and explanations are written as # comments. If these are found lacking, please open a discussion.

Notebooks should be followed in order. The exception is if you wish to predict a GEDI DTM (Digital Terrain Model) to replace the GLO-30 DSM for topographic features. The DSM embeds vegetation height, which confounds alternative scenario predictions when used as a static feature. The DTM workflow:

1. Add `elev_lowestmode` from GEDI L4A in 2_targets.
2. Use 3_features_topo to create initial topographic features from the GLO-30 DSM.
3. Include LCLUC features up to 2015 (the final year of TanDEM-X data acquisition). The difference between DSM and DTM is largely canopy height, so features and model architecture mirror the AGBD workflow.
4. Run 4_datasets, 5_models and 6_scenarios, predicting a single unmasked raster.
5. Return to 3_features_topo and switch to the DTM for a few post-processing steps.
6. Recalculate topographic features using the DTM in place of the DSM.
7. Continue the main AGBD workflow from 4_datasets, selecting the DTM topographic features.

## Citation

The framework's manuscript is currently under development. For now, if you use MASFI in your research, please cite:

Kelly, J., Ong, D.J., Clements, G.R., Low, R., Senescall, M., Zeng, Y., Rao, S., & Jinggut, T. (2026). Mapping alternative scenarios of forest intactness: A cloud-based machine learning framework. https://github.com/joekelly211/masfi
