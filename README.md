# MASFI: Mapping Alternate Scenarios of Forest Intactness

MASFI is a cloud-based machine learning framework for predicting current and alternate scenarios of aboveground biomass density (AGBD). The framework uses XGBoost regression and remote sensing data such as GEDI LiDAR to create high-resolution maps and statistics, supporting protected area planning and forest management.

## Framework Components

1. Project area delineation and template creation
2. GEDI data processing and quality filtering
3. Feature engineering, split into notebooks for topography and land-cover-land-use-change
4. Dataset compilation
5. Model optimisation and SHAP interpretation
6. Scenario creation
7. Predictions with uncertainty and disturbance / intactness
8. Statistics and Sankey diagrams


## Outputs

- Current and alternate scenario AGBD maps
- Forest disturbance and intactness maps
- Percentage uncertainty maps
- Area-specific AGBD and intactness statistics
- Area-specific sankey diagrams of AGBD disturbance

## Requirements

- A familiarity with Python and Google Colab. The workflow is largely automated, but will require editing of some variables for different use-cases.
- Google Account with at least 20 GB Drive. ~100 GB - 2 TB is more realistic for most project areas, with GEDI downloads taking the majority of space. The total amount required for GEDI will be indicated before downloading.
- A Colab subscription is not required but highly recommended for faster runtimes and higher RAM to accommodate larger project areas. The pro+ subscription will also allow background processing.
- The project area should ideally be within GEDI coverage (51.6°N to 51.6°S) and the Tropical Moist Forest biome. The workflow can be adapted other spatial targets besides GEDI or different land-cover data, but this requires a little more proficiency with Python.

## Getting Started

1. Prepare a project area polygon as a .gpkg.
2. Download the notebooks and place in an empty Google Drive folder or Shared Drive.
3. Open the notebooks in Google Colab.
4. Follow the step-by-step instructions in each notebook.

## Citation

If you use MASFI in your research, please cite:
Kelly, J., Clements, G. R., Ong, D.J., Rao, S., Low, R., Senescall, M. & Jinggut, J. (2025). MASFI: Mapping Alternate Scenarios of Forest Intactness. https://github.com/joekelly211/masfi

## Support

For questions and support, please open an issue in this repository or contact the corresponding author at joekelly2119@gmail.com. Responses might be slow January - April 2025 due to sabbatical.
