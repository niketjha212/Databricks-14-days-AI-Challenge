# Day-0 : Setup and Loading (Prerequisites)

### Overview:
- Before starting Day 1, complete this setup to load the e-commerce dataset directly from Kaggle into your Databricks workspace.
- Just completed Day 0 of the Databricks 14 Days AI Challenge by Indian Data Club and Codebasics.

---

### Tasks Done:
- Configured Databricks Free Edition + Kaggle API integration
- Workspace ready and massive dataset ingested
- Created Unity Catalog schema and volume
- Downloaded & extracted multi-category ecommerce dataset 
- Loaded both Oct & Nov 2019 files into Spark DataFrames

---

## Databricks Environment Set-up - Step by step guidance:

1️⃣ Create Databricks account
- Sign up for Databricks Free (Community Edition)
- Log in and create a Python notebook

2️⃣ Generate Kaggle API token
- Kaggle → Account → API → Create New Token
- This downloads kaggle.json

3️⃣ Upload kaggle.json to Databricks
- Upload the file to Databricks (used to configure Kaggle access)

---

### 📦 Dataset Setup:

➡️ Install Kaggle
- %pip install kaggle

➡️Configure Kaggle API
import os
os.environ["KAGGLE_USERNAME"] = "your_kaggle_username"
os.environ["KAGGLE_KEY"] = "your_kaggle_api_key"

➡️Create Schema (Unity Catalog)
spark.sql("""
CREATE SCHEMA IF NOT EXISTS workspace.ecommerce
""")

➡️Create Volume (raw data storage)
spark.sql("""
CREATE VOLUME IF NOT EXISTS workspace.ecommerce.ecommerce_data
""")

➡️Download dataset into Volume
%sh
cd /Volumes/workspace/ecommerce/ecommerce_data
kaggle datasets download -d mkechinov/ecommerce-behavior-data-from-multi-category-store

➡️Unzip and clean
%sh
cd /Volumes/workspace/ecommerce/ecommerce_data
unzip -o https://lnkd.in/g-MFjfHx
rm -f https://lnkd.in/g-MFjfHx
ls -lh

- If all the steps are followed correctly, the data will now appear in **Workspace → Catalog** and is ready to be used with **Spark**.

---

### 💡 Limitations:
- Databricks Free Edition has **limitations with local disk and DBFS**, making large file uploads and CSV downloads unreliable.
- Compute resources are **quota-based and may stop automatically**, which can interrupt long-running data ingestion or processing tasks.

---

### 📚 Learning References & Acknowledgements:

This learning initiative is supported by the data community and learning resources from:
- Databricks: https://www.databricks.com
- Codebasics: https://www.codebasics.io
- Indian Data Club: https://indiandataclub.com

---

### 🔖 Tags & Mentions:
#Databricks #Codebasics #IndianDataClub
