# Irregular Machine Parts Sales Forecasting

## 📌 Project Overview

This project focuses on forecasting irregular sales of machine parts using both local and global forecasting approaches.

The main objective was to compare whether models trained separately for individual products can outperform global machine learning models that use information from multiple products together.

The analysis was based on real sales data from a company operating in the machine parts industry. The dataset contains highly irregular sales patterns, including long periods without sales, varying intervals between transactions, short product histories, and occasional high-volume observations.

The project combines classical intermittent demand forecasting methods with machine learning models in order to evaluate which approach is better suited to this type of sales data.

---

## 📊 Dataset

- Source: real sales data provided by a company
- Period: January 2020 – December 2025
- Original data: 468 products from 20 product groups
- Products selected for modelling: 105
- Product groups included in modelling: 17
- Time frequency: monthly
- Target variable: monthly sales volume

Only products with a sufficiently long sales history were included in the forecasting stage.

---

## 🔍 Exploratory Data Analysis

The exploratory analysis focused on understanding the structure and irregularity of the sales data.

The main steps included:

- analysis of sales frequency across products
- identification of months with zero sales
- analysis of differences between product groups
- examination of sales distributions
- detection of extreme observations and outliers
- analysis of product sales history length
- evaluation of variability in monthly sales volumes
- identification of characteristics typical of intermittent demand

The analysis showed considerable differences between products and confirmed that the dataset was characterized by irregular and intermittent sales patterns.

---

## ⚙️ Data Preprocessing

Before modelling, the data was prepared to ensure consistency and comparability between forecasting methods.

The main preprocessing steps included:

- data cleaning and standardization
- aggregation of sales data to monthly frequency
- creation of complete monthly product panels
- handling extreme observations using winsorization
- filtering products based on the minimum required sales history
- chronological train-test split

The data was divided chronologically to prevent information from future periods from being used during model training.

---

## 🔄 Forecasting Approaches

Two forecasting approaches were compared:

### Local Forecasting

Local models were built separately for each product.

The following methods were used:

- Naive model based on a complete monthly panel
- Naive model based only on months with observed sales
- Moving Average
- Croston method
- SBA
- TSB

Croston, SBA, and TSB were included because they are specifically designed for intermittent demand forecasting.

### Global Forecasting

Global models were trained using information from multiple products simultaneously.

A two-stage modelling approach was applied.

**Stage 1 – Classification**

A LightGBM classifier estimated the probability that a sale would occur in a given month.

**Stage 2 – Regression**

The expected sales volume was estimated using:

- Ridge Regression
- Random Forest
- LightGBM Regressor
- Naive method

The final forecast was obtained by combining the probability of a sale occurring with the estimated sales volume.

---

## 📏 Evaluation Metrics

Forecast accuracy was evaluated using several complementary metrics:

- MAE – Mean Absolute Error
- RMSE – Root Mean Squared Error
- sMAPE – Symmetric Mean Absolute Percentage Error
- MASE – Mean Absolute Scaled Error
- Median MASE across products

Using multiple metrics made it possible to evaluate the models from different perspectives and avoid selecting a model based on a single error measure.

For the LightGBM classifier, the following classification metrics were also analysed:

- Accuracy
- Precision
- Recall
- F1-score
- ROC AUC

---

## 📈 Results

The results showed that local forecasting methods generally achieved better performance than global models.

Among the local methods:

- **SBA** achieved the lowest mean MASE and also the lowest MAE and RMSE
- **Croston** achieved the lowest median MASE
- **TSB** achieved the lowest sMAPE

These three methods clearly outperformed simpler local approaches such as naive models and moving average.

Among the global models:

- the variant combining LightGBM classification with the naive method achieved the lowest mean MASE
- the LightGBM regression variant achieved the lowest median MASE and sMAPE and frequently outperformed the benchmark for individual products
- Ridge Regression achieved the lowest MAE and RMSE among the global models

No single global model was the best according to all evaluation metrics.

---

## 🏆 Main Findings

The comparison showed that local models designed specifically for intermittent demand were the most effective for the analysed dataset.

The best overall results were achieved by:

**SBA, Croston, and TSB**

with SBA providing the strongest overall performance according to mean MASE.

However, global models still achieved competitive results for some individual products. This suggests that the best forecasting method may depend on the characteristics of a specific product or product group.

---

## 💡 Key Insights

- Machine parts sales are highly irregular and contain many zero-sales periods
- Intermittent demand methods perform particularly well for this type of data
- More complex machine learning models do not automatically provide more accurate forecasts
- Using information from multiple products does not necessarily outperform product-specific forecasting
- Global models can still be useful for selected products
- Forecast evaluation should rely on several error metrics rather than a single measure
- Forecasting methods should ideally be selected according to the characteristics of individual products
- A practical forecasting system could combine several models and automatically select the most suitable one for each product

---

## ⚠️ Limitations

The analysis has several limitations:

- data came from a single company
- only selected product groups were included
- only products with sufficient sales history were used for modelling
- information about prices, promotions, delivery times, inventory levels, and product availability was not available
- results depend on methodological choices such as monthly aggregation, winsorization, and model parameters
- models were evaluated mainly using statistical forecasting metrics rather than direct economic costs of forecasting errors

---

## 🛠️ Technologies

- Python
- Pandas
- NumPy
- Scikit-learn
- LightGBM
- Matplotlib
- Seaborn
- Jupyter Notebook

---

## 🚀 Conclusion

The project demonstrates that greater model complexity does not necessarily lead to better forecasting performance.

For the analysed machine parts sales data, local methods specifically designed for intermittent demand achieved the best overall results. In particular, SBA, Croston, and TSB outperformed the global machine learning models across the most important evaluation criteria.

At the same time, the results varied between individual products, showing that there is no single forecasting method that is optimal for the entire product portfolio.
