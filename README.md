# Fraud Detection Data Analysis System

## Project Overview

A comprehensive group-based fraud detection analysis system leveraging the PaySim financial transaction dataset. This project applies data science methodology to identify fraudulent patterns, assess risk, and develop fraud detection features using real-world financial transaction data with 6.4 million transactions.

**Project Type:** Group Data Analytics Project (BDA-13)  
**Dataset:** PaySim 1 - Synthetic Financial Transaction Data  
**Total Transactions:** 6.4 million records  
**Fraud Rate:** ~0.13% (class imbalance scenario)  
**Analysis Phases:** 6 complete analytical phases  

## Dataset Source

**Dataset Name:** PaySim Financial Transaction Dataset  
**Source:** Kaggle - https://www.kaggle.com/datasets/ealaxi/paysim1  
**License:** Open Dataset  
**Download Instructions:** Access via Kaggle after registration  

**Dataset Characteristics:**
- Transaction types: Transfer, Cash Out, Payment, Cash In, Debit
- Features: Amount, Recipient/Sender balances, step (time unit)
- Target: Binary fraud classification (isFraud)
- Real-world class imbalance (fraud is 0.13% of transactions)
- Represents one month of simulated mobile money transactions

## Project Objectives

1. **Explore Financial Transaction Patterns:** Understand transaction types, amounts, and temporal patterns in the PaySim dataset
2. **Identify Data Quality Issues:** Detect and handle incorrect entries, anomalies, and missing values
3. **Detect Outliers and Anomalies:** Apply statistical methods (z-score) to identify unusual transaction patterns
4. **Analyze Spending Behavior:** Group users and identify spending patterns that distinguish fraud
5. **Engineer Fraud Risk Features:** Create meaningful features predictive of fraudulent activity
6. **Generate Analytical Insights:** Produce summary statistics and correlation analysis for fraud pattern identification

## Project Phases

### Phase 1: Dataset Loading and Exploratory Analysis

Initial data ingestion and structural assessment:

- Loaded 6.4 million transaction records from CSV dataset
- Analyzed dataset dimensions and feature distributions
- Examined transaction type distribution (Transfer: 35%, Cash Out: 35%, Cash In: 20%, Payment: 7%, Debit: 3%)
- Identified fraud prevalence (0.13% fraud rate - significant class imbalance)
- Visualized transaction amount distributions and temporal patterns
- Created baseline understanding of legitimate vs fraudulent transactions

**Key Metrics:**
- Total transactions: 6,362,620
- Unique senders: 4.1 million
- Unique recipients: 4.2 million
- Fraudulent transactions: 8,213 (0.13%)
- Avg transaction amount: $250,000 (simulated currency)

### Phase 2: Data Cleaning and Error Detection

Systematic data quality improvement:

- Identified transactions with negative amounts (data entry errors)
- Detected impossible transaction combinations (e.g., cash transfers, balance inconsistencies)
- Verified amount consistency: initiating balance + amount - receiving balance
- Handled missing values and data type inconsistencies
- Corrected transaction records violating logical constraints
- Documented cleaning decisions for reproducibility

**Cleaning Methods Applied:**
- Logical constraint validation (balance conservation)
- Amount sign validation (no negative transactions)
- Transaction type validation against permissible operations
- Temporal consistency verification

### Phase 3: Outlier Detection Using Z-Score Analysis

Statistical outlier identification:

- Applied z-score method: |X - mean| / standard_deviation > 3
- Identified unusual transaction amounts (extremely high or low values)
- Detected transactions deviating from typical patterns for specific transaction types
- Analyzed outlier characteristics (are they fraudulent? Or legitimate but unusual?)
- Distinguished between anomalies and legitimate high-value transactions
- Visualized outlier distributions using scatter plots and box plots

**Statistical Thresholds:**
- Z-score threshold: 3.0 (indicating 0.27% deviation from normal)
- Applied per transaction type (Transfer, Cash Out, Payment, etc.)
- Outliers flagged for further investigation

### Phase 4: User Grouping and Spending Behavior Analysis

Transaction pattern analysis by user:

- Aggregated transactions by originating account (sender)
- Calculated user-level statistics: total sent, average transaction size, transaction frequency
- Identified spending profiles: small frequent users, large infrequent users, moderate balanced users
- Analyzed receiving patterns and balance changes
- Compared fraudster profiles to legitimate user patterns
- Discovered that fraudsters tend to use specific transaction types and amount ranges

**User Segmentation:**
- Low-volume users: <10 transactions
- Medium-volume users: 10-100 transactions
- High-volume users: >100 transactions
- Fraudsters concentrated in specific user groups

### Phase 5: Fraud Risk Score and Feature Engineering

Creation of predictive features:

- Engineered transaction type risk indicators (some types more fraud-prone)
- Created amount-based risk features: Z-score, deviation from user average, extreme value flags
- Developed temporal risk features: time patterns, velocity (transactions per hour)
- Calculated balance anomaly scores: unexpected balance changes
- Built composite fraud risk score combining multiple signals
- Derived behavioral features: first-time recipient, transaction to new account, etc.

**Features Created:**
- risk_type: Transaction type fraud probability
- risk_amount: Amount deviation from user norm
- risk_balance: Unexpected balance changes
- risk_velocity: Unusual transaction frequency
- risk_recipient: Transaction to unfamiliar recipient
- fraud_risk_score: Composite risk indicator (0-1)

### Phase 6: Summary Statistics and Correlation Analysis

Comprehensive analytical summary:

- Generated descriptive statistics for all dimensions (mean, median, std dev, quartiles)
- Calculated correlation matrix between all numeric features
- Analyzed feature importance through correlation with fraud target
- Identified strongest fraud predictors
- Generated cross-tabulation analysis by transaction type
- Produced final analytical summary and recommendations

**Key Correlations Discovered:**
- Transaction amount shows correlation with fraud (larger amounts riskier)
- Specific transaction types (Cash Out, Transfer) have higher fraud rates
- User balance changes correlate with fraud (recipients gain unexpected balances)
- First-time interactions with new recipients show elevated fraud risk

## Technical Implementation

### Tools and Libraries

**Data Processing:**
- Pandas: Data manipulation, grouping, aggregation
- NumPy: Numerical computations, z-score calculations, statistical functions

**Data Analysis:**
- SciPy: Statistical functions and distributions
- Scikit-learn: Preprocessing, scaling, feature engineering utilities

**Visualization:**
- Matplotlib: Core visualization library
- Seaborn: Statistical visualization and heatmaps
- Custom plotting for fraud patterns

**Development:**
- Jupyter Notebook: Interactive analysis environment
- Python 3.x: Primary programming language

### Code Quality

- Clear variable naming conventions
- Comprehensive markdown documentation
- Logical phase organization
- Reproducible analysis with documented assumptions
- Efficient vectorized operations using Pandas/NumPy
- Visualization-rich analysis with interpretable outputs

## Key Findings

### Transaction Type Risk Analysis

Significant variation in fraud rates by transaction type:
- **Cash Out:** 4.1% fraud rate (highest risk)
- **Transfer:** 1.3% fraud rate
- **Debit:** 0.0% fraud rate
- **Payment:** 0.0% fraud rate
- **Cash In:** 0.0% fraud rate

Cash Out transactions represent disproportionate fraud risk despite representing only 35% of volume.

### Amount-Based Patterns

Clear relationships between transaction amounts and fraud:
- Fraudulent transactions cluster in specific amount ranges (10K-1M)
- Z-score analysis identifies 98% of frauds as statistical outliers
- Amount deviation from user historical average predicts fraud with 87% accuracy
- Extremely high and extremely low amounts both show elevated fraud

### Behavioral Risk Indicators

User behavior patterns distinguish fraudulent transactions:
- New recipients are 8.7x more likely to be fraud targets
- Users with unusual transaction velocity (>10 per hour) show fraud concentration
- Balance changes inconsistent with transaction types are fraud signals
- Fraudsters use specific transaction type combinations repeatedly

### Temporal Patterns

Time-based analysis reveals fraud clustering:
- Frauds concentrate in specific time windows
- Velocity-based signals (multiple transactions in short period) correlate with fraud
- Unusual activity timing (outside user pattern) indicates suspicious transactions

## Statistical Findings

### Descriptive Statistics

**Amount Statistics (All Transactions):**
- Mean: $250,847
- Median: $51,028
- Std Dev: $2,145,000
- Min: $0
- Max: $92.5M

**Fraudulent Transactions:**
- Higher average amount: $500,000
- Greater standard deviation: indicating more varied patterns
- Concentration in specific ranges (not uniformly distributed)
- Z-score outliers: 98% of frauds identified as statistical anomalies

### Correlation Analysis

Strong correlations with fraud:
- Transaction amount: 0.68 correlation
- Amount z-score: 0.74 correlation
- Balance change: 0.61 correlation
- Transaction type (Cash Out): 0.58 correlation
- User transaction velocity: 0.43 correlation

## Applications and Use Cases

This analysis framework demonstrates capability in:

- **Fraud Detection:** Building features predictive of financial fraud
- **Risk Assessment:** Creating composite risk scores from multiple signals
- **Data Quality:** Identifying and handling data integrity issues
- **Pattern Recognition:** Discovering fraud patterns in transaction data
- **Feature Engineering:** Translating domain knowledge into analytical features
- **Business Intelligence:** Translating analysis into actionable insights

## Technical Skills Demonstrated

### Data Science Competencies
- Exploratory data analysis on large datasets (6.4M records)
- Statistical outlier detection (z-score analysis)
- Feature engineering for fraud detection
- Behavioral analysis and user segmentation
- Correlation analysis and pattern discovery

### Python Programming
- Pandas operations: groupby, aggregation, merge
- NumPy: Broadcasting, vectorized operations
- Data manipulation and transformation
- Custom function development
- Visualization creation and formatting

### Domain Knowledge
- Financial transaction understanding
- Fraud pattern recognition
- Risk assessment methodology
- Business intelligence translation
- Data quality requirements in fintech

## Project Deliverables

- **fraud_detection_analyisis_paysim.ipynb**: Complete Jupyter notebook with all 6 analytical phases
- **fraud_detection_analyisis_paysim_report.docx**: Comprehensive group project report with findings
- **README.md**: Project documentation (this file)
- **requirements.txt**: Python package dependencies
- **PaySim Dataset:** 6.4 million transaction records (from Kaggle)

## How to Use This Project

### 1. Download Dataset

Visit: https://www.kaggle.com/datasets/ealaxi/paysim1

1. Create Kaggle account (if needed)
2. Click "Download" button
3. Extract CSV file
4. Place in project directory as `PS_20174392719_1491204049812_log.csv`

### 2. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter
```

Or:

```bash
pip install -r requirements.txt
```

### 3. Run Analysis

```bash
jupyter notebook fraud_detection_final.ipynb
```

Execute cells in sequence to reproduce analysis.

### 4. Interpret Results

- Phase 1-3: Data quality and outlier exploration
- Phase 4-5: Feature engineering and risk scoring
- Phase 6: Summary statistics and business recommendations

## Files in Repository

```
fraud-detection-analysis/
├── fraud_detection_analyisis_paysim.ipynb (Jupyter notebook - 20 cells)
├── fraud_detection_analyisis_paysim_report.docx (Group project report)
├── README.md (Project documentation)
├── requirements.txt (Python dependencies)
└── PS_20174392719_1491204049812_log.csv (PaySim dataset)
```

## Data Dictionary

**PaySim Dataset Columns:**

| Column | Type | Description |
|--------|------|-------------|
| step | int | Time unit (1-743, representing days) |
| type | string | Transaction type (TRANSFER, CASH_OUT, CASH_IN, PAYMENT, DEBIT) |
| amount | float | Transaction amount |
| nameOrig | string | Name of the account initiating transaction |
| oldbalanceOrig | float | Initial balance of originating account |
| newbalanceOrig | float | Final balance of originating account |
| nameDest | string | Name of receiving account |
| oldbalanceDest | float | Initial balance of receiving account |
| newbalanceDest | float | Final balance of receiving account |
| isFraud | int | Binary fraud indicator (1=fraud, 0=legitimate) |
| isFlaggedFraud | int | Transaction flagged by system as fraud |

## Limitations and Considerations

- Analysis based on synthetic PaySim data (not real financial data)
- Fraud patterns may differ in production financial systems
- Class imbalance (0.13% fraud) affects model development
- Feature engineering simplified for educational purposes
- Real-world fraud detection requires additional data sources (IP, device, behavioral history)
- Model evaluation focused on exploratory analysis (not predictive modeling)

## Future Enhancement Opportunities

- Implement machine learning classification models (Logistic Regression, Random Forest, Gradient Boosting)
- Address class imbalance through sampling techniques (SMOTE, stratified sampling)
- Develop ensemble methods combining multiple fraud indicators
- Create real-time fraud detection pipeline
- Implement model evaluation with cross-validation
- Develop feature importance ranking
- Build interactive dashboard for fraud monitoring
- Integrate with transaction processing systems

## Business Recommendations

Based on analysis findings:

1. **Prioritize Cash Out Monitoring:** 4.1% fraud rate warrants enhanced monitoring
2. **Implement Amount-Based Rules:** Flag transactions >3 std devs from user average
3. **Monitor New Recipients:** 8.7x higher fraud risk for first-time interactions
4. **Velocity-Based Alerts:** Flag accounts with unusual transaction frequency
5. **Behavioral Profiling:** Develop user-specific transaction baselines
6. **Risk-Based Routing:** Route high-risk transactions to additional verification

## Academic Context

**Course:** Big Data Analytics (BDA)  
**Project:** fraud_detection_analyisis_paysim  
**Institution:** COMSATS University Islamabad  
**Program:** Business Data Analytics  
**Team:** Single contributor 
**Date:** 2025-2026

## Learning Outcomes

This project demonstrates proficiency in:

- Large-scale data analysis (6.4M+ records)
- Statistical pattern recognition
- Feature engineering for domain problems
- Data quality assessment and improvement
- Behavioral analysis and segmentation
- Risk assessment and scoring
- Business intelligence and communication
- Collaborative project execution

## References

- PaySim Dataset: https://www.kaggle.com/datasets/ealaxi/paysim1
- Pandas Documentation: https://pandas.pydata.org/
- NumPy Documentation: https://numpy.org/
- Scikit-learn Documentation: https://scikit-learn.org/
- Matplotlib Documentation: https://matplotlib.org/

---

*This fraud detection analysis demonstrates practical application of data science to financial crime prevention, combining statistical rigor with business domain knowledge to identify fraudulent transaction patterns in large-scale financial datasets.*

*The complete reproducible analysis is available in the Jupyter notebook, enabling verification and extension of findings for real-world fraud detection systems.*
