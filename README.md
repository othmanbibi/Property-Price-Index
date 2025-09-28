# Real Estate Price Index (REPI) Project

A statistical analysis project implementing the Repeat Sales Method to construct quarterly real estate price indices, inspired by the Moroccan Central Bank's approach to property price monitoring.

## Overview

This project analyzes Connecticut real estate transaction data from 2001-2022 to construct comprehensive price indices using econometric methods. The implementation follows the methodology outlined in the Irving Fisher Committee paper "Constructing a real estate price index: the Moroccan experience" by Assil EL MAHMAH.

## Dataset

- **Source**: Connecticut Real Estate Sales 2002-2022
- **Size**: 1,097,629 property transactions
- **Period**: 2001-2023 (22 years)
- **Coverage**: 170 towns across Connecticut

### Data Features
- Serial Number
- Date Recorded
- Town/Location
- Property Address
- Assessed Value
- Sale Amount
- Sales Ratio
- Property Type (Residential, Commercial, Vacant Land, Apartments, Industrial, Public Utility)
- Residential Type (Single Family, Two Family, Three Family, Four Family, Condo)

## Methodology

### Repeat Sales Method (RSM)

The project implements the Repeat Sales Method, which:
- Focuses on properties sold multiple times during the study period
- Eliminates heterogeneity bias by comparing the same property over time
- Constructs price indices based on logarithmic price changes
- Uses only 124,408 repeat sales from the original dataset (13.5% of properties)

### Mathematical Framework

The core regression model:
```
log(P_it/P_iτ) = Σ β_s * D_is + ε_iτ
```

Where:
- `P_it`: Price of property i at time t (second sale)
- `P_iτ`: Price of property i at time τ (first sale)  
- `β_s`: Coefficient for period s
- `D_is`: Dummy variable matrix
- `ε_iτ`: Error term

Index construction:
```
I_t = 100 * exp(β̂_t - β̂_τ)
```

## Data Processing Pipeline

### 1. Data Cleaning
- Handle missing values using mean imputation by town and property type
- Remove properties with missing addresses (51 records)
- Eliminate outliers using IQR method on log-transformed prices
- Final dataset: 995,169 clean transactions

### 2. Property Classification
- Standardize property types and residential categories
- Map inconsistent entries to unified categories
- Create hierarchical classification system

### 3. Repeat Sales Identification
- Group transactions by property address and type
- Identify properties with multiple sales (124,408 pairs)
- Create time-series dummy variables for quarterly analysis

### 4. Model Implementation
- Linear regression using statsmodels OLS
- Quarterly dummy variables (2001 Q1 - 2022 Q4)
- Separate indices for different property types

## Key Results

### Price Index Trends
- **2001-2008**: Generally upward trend with volatility
- **2008-2012**: Decline following financial crisis
- **2012-2020**: Recovery and stabilization
- **2020-2022**: Mixed signals with some decline

### Property Type Performance
Different property categories show varying price trajectories:
- Residential properties form the majority of transactions
- Commercial and industrial properties show different cyclical patterns
- Vacant land prices demonstrate higher volatility

## Technical Implementation

### Libraries Used
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computations
- **statsmodels**: Econometric modeling
- **matplotlib/seaborn**: Data visualization
- **Prophet**: Time series forecasting
- **ISLP**: Statistical learning tools

### Code Structure
```
├── Data Import & Cleaning
├── Missing Value Treatment
├── Outlier Detection & Removal
├── Repeat Sales Identification
├── Model Matrix Construction
├── OLS Regression Implementation
├── Index Calculation
├── Forecasting with Prophet
└── Visualization & Export
```

## Forecasting Component

The project includes a forecasting module using Facebook's Prophet:
- Extends historical trends 20 quarters into the future
- Incorporates seasonality patterns
- Provides confidence intervals for predictions
- Automated quarterly forecasting pipeline

## Limitations & Considerations

1. **Selection Bias**: Only 13.5% of properties have repeat sales
2. **Quality Changes**: Method assumes property quality remains constant between sales
3. **Market Representation**: Repeat sales may not represent the broader market
4. **Data Completeness**: Some property characteristics unavailable
5. **Geographic Coverage**: Limited to Connecticut market

## Applications

This REPI system can be used for:
- **Monetary Policy**: Central bank analysis of real estate market conditions
- **Financial Stability**: Banking sector risk assessment
- **Economic Research**: Market cycle analysis and forecasting
- **Real Estate Valuation**: Property appraisal and investment decisions
- **Academic Studies**: Econometric methodology validation

## Files Structure

- `Real_estate_price_index.pdf`: Complete analysis notebook
- `STAT.pdf`: Reference methodology paper
- Various Excel exports with indices and forecasts
- Automated data processing functions

## Future Enhancements

1. **Hedonic Method Implementation**: When more property characteristics become available
2. **Geographic Expansion**: Extension to other states/regions
3. **High-Frequency Updates**: Monthly or weekly index construction
4. **Quality Adjustment**: Methods to account for property improvements
5. **New Construction Index**: Separate tracking of newly built properties

## References

Based on the methodology from:
- EL MAHMAH, Assil. "Constructing a real estate price index: the Moroccan experience." Irving Fisher Committee on Central Bank Statistics, IFC Working Papers No 9, March 2013.
- Case, K.E., & Shiller, R.J. (1989). "The efficiency of the market for single family homes." American Economic Review.
- Bailey, M.J., Muth, R.F., Nourse, H.O. (1963). "A regression method for real estate price index construction." Journal of the American Statistical Association.

## License

This project is for educational and research purposes. Please cite appropriately if used in academic work.

---

*Note: This implementation serves as both a statistical analysis exercise and a foundation for developing real estate price monitoring systems.*
---
You can reach me at [Othman.BIBI@emines.um6p.ma](Othman.BIBI@emines.um6p.ma)
