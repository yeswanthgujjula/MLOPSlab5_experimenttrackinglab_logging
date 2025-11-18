# MLOps Lab 5 – Logging with Energy Dataset

This lab applies Python’s `logging` module to a small ML pipeline built on the
`energydata_complete.csv` dataset.

The pipeline includes:
- loading the dataset
- data quality checks and cleaning
- feature engineering
- model training and evaluation
- writing logs to separate log files

---

## Dataset

**File:** `energydata_complete.csv`  

Main columns used:
- `date` – timestamp  
- `Appliances` – target (energy use of appliances)  
- `lights` – energy used by lights  
- `T1`, `RH_1` – indoor temperature and humidity  
- `T_out`, `RH_out` – outdoor temperature and humidity  
- `Windspeed` – wind speed  

`Appliances` is used as the prediction target.

---

## Logging Setup

Three loggers are used:

1. **Pipeline logger** – `energy_pipeline`  
   - High-level run information  
   - File: `logs/main/pipeline.log`

2. **Data logger** – `energy.data`  
   - Dataset loading, checks, cleaning, feature engineering  
   - File: `logs/data/data_steps.log`

3. **Model logger** – `energy.model`  
   - Train/test split, model training, evaluation metrics  
   - File: `logs/model/model_steps.log`

Each logger writes both to the console and to its own log file.

---

## Notebook: `lab5.ipynb`

Main steps in the notebook:

1. **Setup & loggers**  
   - Create `logs/main`, `logs/data`, `logs/model`  
   - Configure `root_logger`, `data_logger`, `model_logger`

2. **Load data**  
   - Upload and read `energydata_complete.csv`  
   - Log shape and column names

3. **Data checks & cleaning**  
   - Convert `date` to datetime  
   - Log missing values  
   - Drop rows with missing `Appliances`  
   - Check for negative values in `Appliances`

4. **Feature engineering**  
   - Create `hour`, `day_of_week`, `is_weekend`  
   - Create `appliances_roll_mean` (rolling mean)  
   - Create `lights_to_appliances_ratio`  
   - Select final feature set for the model

5. **Model training & evaluation**  
   - Split into train and test sets  
   - Train `RandomForestRegressor`  
   - Log MAE and R²

6. **Log inspection**  
   - Use `!tail` to display the last lines of each log file inside the notebook.

---

## How to Run (Google Colab)

1. Open `lab5.ipynb` in Google Colab.  
2. Run all cells from top to bottom.  
3. When prompted, upload `energydata_complete.csv`.  
4. Check the `logs/` folder or the final cells to view the log outputs.

