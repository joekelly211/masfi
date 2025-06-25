# MASFI: Mapping Alternate Scenarios of Forest Intactness

A cloud-based machine learning framework. MASFI supports protected area planning, monitoring and management using remote sensing data such as GEDI LiDAR aboveground biomass density.

## Framework Components

- 1_areas: Project area delineation, with raster template creation based on Copernicus GLO-30 DEM.
- 2_targets: GEDI data download, processing and quality filtering, with support for user data upload.
- 3_features_lcluc: Feature download and engineering for land-cover-land-use-change.
- 3_features_topo: Feature engineering for topographic metrics.
- 4_datasets: Spatial and temporal matching of targets and features.
- 5_models: XGBoost model optimisation and validation, with SHAP feature interpretation
- 6_scenarios: Historic and alternate scenario creation with simple prediction outputs
- 7_uncertainty: Scenario prediction using a multi-model Monte Carlo approach, with outputs including mean and uncertainty
- 8_differences: Calculations of disturbance and intactness using differences between scenarios
- 9_statistics: Area-based statistics using uploaded polygons, with Sankey diagrams visualising changes attributable to disturbance.

## Requirements

- A familiarity with Python, Google Colab and Google Drive. The workflow is largely automated, but will require editing of some variables for different use-cases.
- Google Account with at least 20 GB Drive. ~100 GB - 2 TB is more realistic for most project areas, depending on spatial extent. GEDI downloads take the majority of the space, and the total amount required for will be indicated before downloads begin.
- A Colab subscription is not required but highly recommended for faster runtimes and more RAM to accommodate larger project areas. The pro+ subscription will also allow background processing.
- The project area should ideally be within GEDI coverage (51.6°N to 51.6°S) and the Tropical Moist Forest biome. The workflow can be adapted other spatial targets besides GEDI or different land-cover data for creating features, but this requires a little more proficiency with Python.

## Getting Started

1. Prepare a project area polygon as a .gpkg.
2. Download the notebooks and place in an empty Google Drive folder or Shared Drive.
3. Open the notebooks in Google Colab.
4. Follow the step-by-step instructions in each notebook. If these are found lacking, please open a discussion.

## Future work

Additional tools with functions such as 'business as usual' forecasting, support for additional biomes, geohazard predictions and vegetation structure classification are currently under development. MASFI will continue to be supported, and if funding and time permits, worked into a larger software suite for protected area prioritisation and management.

## Citation

If you use MASFI in your research, please cite:
Kelly, J., Clements, G. R., Ong, D.J., Low, R., Senescall, M., Zeng, Y.W., Rao, S., & Jinggut, T. (2025). Mapping alternate scenarios of forest intactness: a machine learning framework. https://github.com/joekelly211/masfi
