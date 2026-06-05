 Content:
   ```
   # PaySim Dataset Download Instructions
   
   ## Dataset Overview
   - Name: PaySim 1 - Synthetic Financial Transaction Data
   - Source: https://www.kaggle.com/datasets/ealaxi/paysim1
   - Size: 2.5 GB (uncompressed)
   - Transactions: 6,362,620 records
   - File: PS_20174392719_1491204049812_log.csv
   
   ## How to Download
   
   1. Create Kaggle account (if needed): https://www.kaggle.com/settings/account
   2. Visit: https://www.kaggle.com/datasets/ealaxi/paysim1
   3. Click "Download" button (requires login)
   4. Accept terms and download will start
   5. Unzip downloaded file
   6. Place CSV in project root directory
   
   ## File Placement
   
   After downloading, place the CSV file in the repository root:
   
   ```
   fraud-detection-analysis/
   ├── fraud_detection_analysis.ipynb
   ├── README.md
   ├── requirements.txt
   └── PS_20174392719_1491204049812_log.csv  ← Place here
   ```
   
   ## Verify Dataset
   
   In Jupyter notebook, run:
   ```python
   import pandas as pd
   df = pd.read_csv('PS_20174392719_1491204049812_log.csv')
   print(df.shape)  # Should show (6362620, 11)
   print(df.head())
   ```
   
   If this runs without error, dataset is properly placed.
   
   ## Alternative: Kaggle API
   
   Advanced users can use Kaggle CLI:
   ```bash
   pip install kaggle
   kaggle datasets download -d ealaxi/paysim1
   unzip paysim1.zip
   ```
   
   See: https://www.kaggle.com/settings/account for API setup
   ```
