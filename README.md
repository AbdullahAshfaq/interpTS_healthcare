# interpTS_healthcare

## Directory Structure

```bash
|-> interp_figs: Visualizations of interpretability of all models on all datasets using all methods
|-> interp_metrics: Interpretability metrics of all methods on all datasets. (_CF=Counterfactual, _faith=faithfulness, ...)
 -> model_metrics/lstm: Performance metrics of all models
```

## How to reproduce

To results of experiments are saved in `interp_figs` and `interp_metrics`. If you want to reproduce these, Follow these steps.

**System Requirements**: 16GB RAM

### 1. Download and install relevant libraries



```bash
# Assuming that pytorch, pandas, numpy and other standard ML libraries are already installed

# Instaling tsinterpret for interpretability methods
pip install tsinterpret

# Installing XTSC for quantative benchmarking 
git clone https://github.com/JHoelli/XTSC-Bench.git
cd ./XTSC-Bench
pip install .
```

### 2. Model Training

Open the `training_models.ipynb` notebook. Change the `dataset` variable to either `['ECG200','ECG5000','Epilepsy']` and run all the cells. For each dataset, 2 models (LSTM, CNN) will be trained. 


```bash
# ECG200 and ECG5000
# CNN
Use default settings
# LSTM
hidden_size=10 # size of hidden layer
rnn=0.1 # dropout

# Epilepsy
# CNN
Use default settings
# LSTM
hidden_size=200
rnn=0.3
```
**Note**: To get the exact same performing model, would need to play with patience of training and epochs a little.


### 3. Applying Interpretability methods

Notebooks for LSTM and CNN models are separate for this. 

Open the `lstm_explain.ipynb` notebook for LSTM and the corresponding for CNN models. Change the `dataset` variable to either `['ECG200','ECG5000','Epilepsy']` and run all the cells. For each dataset, 4 plots will be generated (one for each interpretability method i.e. TSEvo, FA, FO, GRAD) and will be saved in `interp_figs`. 

### 4. Quantitative Evaluation

Notebooks for LSTM and CNN models are separate for this. 

Open the `lstm_benchmarks.ipynb` notebook for LSTM and the corresponding for CNN models. Change the `dataset` variable to either `['ECG200','ECG5000','Epilepsy']` and run all the cells. For each dataset, 4 csvs will be generated (one for each metric category i.e. Coutnerfactual(CF), Faithfulness, Reliability, Complexity) and will be saved in `interp_metrics`.

### 5. Visualizing Quantative results

To plot charts to compare various metrics for all models and datasets, run the notebook `results_viz.ipynb` with classifier `(lstm, cnn)` and dataset `['ECG200','ECG5000','Epilepsy']`. It will take the csv results generated in the last step and plot them. The plots are saved in `interp_metrics`.


