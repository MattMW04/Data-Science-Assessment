# Data Science Assessment: Diabetes Dataset Analysis

This project demonstrates a full data science workflow using a diabetes dataset. The workflow includes:

- **Data Exploration & Cleaning:**  
  - Initial exploration of the raw dataset to identify missing or invalid values.
  - Replacement of impossible zero values with NaN for relevant columns.
  - Removal of columns with excessive missing data (e.g., Insulin, SkinThickness).
  - Imputation of missing values in remaining columns using mean values.
  - Removal of unnecessary columns (e.g., Id).

- **Data Analysis & Visualization:**  
  - Univariate, bivariate, and multivariate analysis using histograms, box plots, scatter plots, and correlation heatmaps.
  - Visualization of distributions and relationships between variables and the diabetes outcome.

- **Model Building & Evaluation:**  
  - Logistic Regression and Random Forest Classifier models are trained to predict diabetes outcome.
  - Feature importance is analyzed to select the most predictive variables.
  - Model performance is evaluated using accuracy, precision, recall, F1-score, and confusion matrices.
  - Decision Tree visualization is included for interpretability.

- **Key Findings:**  
  - The most predictive variables for diabetes classification are Glucose, BMI, BloodPressure, and Age.
  - Random Forest Classifier achieved the highest accuracy and balanced recall for both classes.

The project is implemented in Jupyter notebooks, with all data cleaning and analysis steps clearly documented and reproducible.

## How to Run

1. **Install Requirements:**  
   Ensure you have Python 3.12 installed. Install required libraries using:
   ```
   pip install requirements.txt
   ```

2. **Open Notebooks:**  
   Open the notebooks (`AssessmentDataCleaning.ipynb` and `Asessment-Data-Usage.ipynb`) in JupyterLab, VS Code, or another Jupyter-compatible environment.

3. **Run Cells:**  
   Execute each cell in order to reproduce the data cleaning, analysis, and modeling steps.

4. **Datasets:**  
   The cleaned dataset is provided in `Datasets/Diabetes-Dataset-Cleaned-2.csv`. The original dataset should be placed in the `Datasets` folder as `Diabetes Dataset.csv` if you wish to repeat the cleaning steps.

5. **Results:**  
   All results, visualizations, and model outputs will be displayed within the notebooks.
