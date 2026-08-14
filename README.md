# MASFI: Mapping Alternative Scenarios of Forest Intactness

A cloud-based machine learning framework for predicting actual and alternative aboveground biomass density (AGBD) at 30 m resolution. MASFI uses GEDI L4A footprints, XGBoost regression and features engineered from the JRC Tropical Moist Forest product to quantify forest disturbance, restoration potential and relative intactness with IPCC-compliant uncertainty estimates. Outputs support protected area delineation, monitoring and management. This framework helped to inform the gazettement of the Al-Sultan Abdullah Royal Tiger Reserve in Pahang, Malaysia. Note that all parameters are currently set at values used this project area, which in most cases make acceptable default values.

## Framework Components

- **1_areas**: Project area delineation and raster template creation from the Copernicus GLO-30 DEM, including pixel area calculation on the WGS84 ellipsoid.
- **2_targets**: GEDI L4A download via NASA CMR API, quality filtering, and extraction of AGBD alongside standard error and elevation. Also supports user data upload (i.e. targets other than GEDI).
- **3_features_lcluc**: Download and engineering of scenario features from the TMF annual classification and disturbance products. Binary rasters are converted to edge distance and local density metrics within a 120 m ecological threshold. Old-growth proxy and forest reserve polygons are rasterised similarly.
- **3_features_topo**: Engineering of static topographic features from a digital elevation model (DEM), either the GLO-30 digital surface model or a GEDI-derived digital terrain model (DTM). Twenty-four topographic metrics (slope, topographic position index, stream power index, etc.) in smoothed and unsmoothed variants. Geographic features (pixel-wise latitude, longitude, distance to coast) are also created here.
- **4_datasets**: Spatial and temporal matching of GEDI footprints with feature rasters.
- **5_models**: XGBoost hyperparameter optimisation using a custom SHAP-guided ('automated') random search evaluation, cross-validation, and SHAP feature interpretation. Supports multi-runtime parallel optimisation.
- **6_scenarios**: Compilation of feature stacks for yearly, undisturbed, disturbance area and recovery scenarios. Scenario features are modified to simulate alternative states while static features remain unchanged.
- **7_predictions**: Predictions with multi-iteration Monte Carlo simulation propagating GEDI L4A standard error through model training to pixel-level 95% confidence intervals (IPCC Approach 2). Accuracy comparison with existing products.
- **8_differences**: Disturbance, restoration potential and percentage loss from scenario differences with uncertainty propagation (IPCC Approach 1 for degradation and recovery, Approach 2 for percentage loss). Quantile-based relative intactness scoring percentage loss on a 1–10 scale.
- **9_statistics**: Area-based aggregation of AGB, disturbance, restoration and intactness statistics by polygon, with Sankey diagrams and yearly trend plots.

## Requirements

- Familiarity with Python, Google Colab and Google Drive. The workflow is largely automated and user-friendly, but requires editing of some variables for different use cases.
- Google Account with at least 20 GB Drive. 100 GB – 2 TB is more realistic for most project areas, depending on spatial extent. GEDI downloads take the majority of the space, and the total required will be indicated before downloads begin.
- A Colab subscription is not required but highly recommended for faster runtimes and more RAM to accommodate larger project areas. The Pro+ subscription also allows background processing, which is especially useful for lengthy hyperparameter optimisation and Monte Carlo iteration predictions.
- The project area should be within GEDI coverage (51.6°N to 51.6°S) and ideally the tropical moist forest biome. The framework can be adapted to other biomes using equivalent forest cover and disturbance products, though modifications to target filtering and scenario design would be needed.
- Old-growth or mature forest proxy polygons within or adjacent to the project area, serving as baselines for intactness. Without these, the earliest available satellite baseline (e.g. 1990s) can be used, with the understanding that the project area intactness will likely overestimated and restoration potential underestimated.

## Getting Started

1. Prepare a project area polygon as a .gpkg, along with any land-use polygons (old-growth protected areas, management units, etc.).
2. Download the notebooks and place in an empty Google Drive folder or Shared Drive (your base_dir).
3. Open the notebooks in Google Colab and modify the base_dir code block at the top. Start with 1_areas and run code blocks sequentially.
4. Instructions and explanations are written as # comments. If these are found lacking, please open a discussion here or contact me at joe@oldgrowthlabs.com.

Notebooks should be followed in order. The exception is if you wish to predict a GEDI DTM to replace the GLO-30 DSM for topographic features. The DSM embeds vegetation height, which confounds alternative scenario predictions when used as a static feature. The DTM workflow in brief:

1. Make sure GEDI L4A 'elev_lowestmode' is included as a parameter in 2_targets, as this will be used in place of 'agbd'.
2. Use the same static features as the AGBD model, calculated using the GLO-30 DSM.
3. Include LCLUC features up to 2015 (the final year of GLO-30's TanDEM-X data acquisition). The difference between DSM and DTM is largely canopy height, so features and model architecture mirror the AGBD workflow.
4. Run 4_datasets, 5_models and 6_scenarios, predicting a single unmasked raster.
5. Return to 3_features_topo and switch from GLO-30 to the DTM, which will run through a few post-processing steps.
6. Recalculate topographic features using the DTM in place of the GLO-30 DSM.
7. Continue the main AGBD workflow from 4_datasets, selecting the DTM topographic features. Your model is should now be less confounded by vegetation embedded in the topography metrics.

## Citation

Two associated articles are currently under review and available as preprints. One manuscript outlines the framework's application to the tiger reserve in Malaysia, providing a concise methods alongside implications for conservation and management:

Kelly, J., Ong, D. J., Clements, G. R., Low, R., Senescall, M., Zeng, Y., Rao, S., & Jinggut, T. (2026b). **Prioritising forest protection and restoration using alternative scenarios of intactness**. SSRN Preprint. [https://doi.org/10.2139/ssrn.7259344](https://doi.org/10.2139/ssrn.7259344)

While a co-submitted methods article provides an in-depth protocol with supporting equations and an expanded design rationale:

Kelly, J., Ong, D. J., Clements, G. R., Low, R., Senescall, M., Zeng, Y., Rao, S., & Jinggut, T. (2026a). **Mapping alternative scenarios of forest intactness: A machine learning framework**. SSRN Preprint. [https://ssrn.com/abstract=7269979](https://ssrn.com/abstract=7269979)

Please cite the relevant publication(s) if you use MASFI in your work.
