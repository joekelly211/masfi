# MASFI: Mapping Alternate Scenarios of Forest Intactness

A cloud-based machine learning framework. It uses XGBoost regression and remote sensing data such as GEDI LiDAR to create high-resolution maps and statistics, supporting protected area planning and management.

## Framework Components

1. Project area delineation and template creation.
2. GEDI data download, processing and quality filtering.
3. Feature engineering, including topography and land-cover-land-use-change.
4. Spatial matching and dataset compilation
5. Model optimisation and SHAP feature interpretation
6. Historic and alternate scenario creation.
7. Predictions with uncertainty of scenarios, disturbance and intactness.
8. Area-based statistics and Sankey diagrams.


## Outputs

- Current and alternate scenario AGBD maps.
- Forest disturbance and intactness maps.
- Percentage uncertainty maps.
- Area-specific AGBD and intactness statistics.
- Area-specific sankey diagrams of AGBD disturbance.

## Requirements

- A familiarity with Python, Google Colab and Google Drive. The workflow is largely automated, but will require editing of some variables for different use-cases.
- Google Account with at least 20 GB Drive. ~100 GB - 2 TB is more realistic for most project areas, depending on spatial extent. GEDI downloads take the majority of the space, and the total amount required for will be indicated before downloads begin.
- A Colab subscription is not required but highly recommended for faster runtimes and more RAM to accommodate larger project areas. The pro+ subscription will also allow background processing.
- The project area should ideally be within GEDI coverage (51.6°N to 51.6°S) and the Tropical Moist Forest biome. The workflow can be adapted other spatial targets besides GEDI or different land-cover data, but this requires a little more proficiency with Python.

## Getting Started

1. Prepare a project area polygon as a .gpkg.
2. Download the notebooks and place in an empty Google Drive folder or Shared Drive.
3. Open the notebooks in Google Colab.
4. Follow the step-by-step instructions in each notebook. If these are found lacking, please open a discussion.

## Citation

If you use MASFI in your research, please cite:
Kelly, J., Clements, G. R., Ong, D.J., Rao, S., Low, R., Senescall, M. & Jinggut, T. (2025). Mapping alternate scenarios of forest intactness: a machine learning framework. https://github.com/joekelly211/masfi

## Support

Please start a 'discussion'.

## Future work

Additional tools with functions such as 'business as usual' forecasting, support for additional biomes, geohazard predictions and vegetation structure classification are currently under development. MASFI will continue to be supported, and eventually worked into a larger software suite for protected area prioritisation and management.
