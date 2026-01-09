# **DAY 1 – Platform Setup & First Steps**

## 📘 Things Learnt:
- Why Databricks vs Pandas/Hadoop?
- Lakehouse architecture basics
- Databricks workspace structure
- Industry use cases (Netflix, Shell, Comcast)

## 🛠️ Tasks Completed:
1. Create Databricks Community Edition account
2. Navigate Workspace, Compute, Data Explorer
3. Create first notebook
4. Run basic PySpark commands

## 📊 Practice with Data:

### Create simple DataFrame:

data = [("iPhone", 999), ("Samsung", 799), ("MacBook", 1299)]

df = spark.createDataFrame(data, ["product", "price"])

df.show()

| Product | Price |
|--------|-------|
| iPhone | 999 |
| Samsung | 799 |
| MacBook | 1299 |



### Filter expensive products:

df.filter(df.price > 1000).show()

|product|price|
|-------|-----|
|MacBook| 1299|



### 🔑 Key Takeaways:
- Databricks provides an integrated **Lakehouse platform** combining data engineering and analytics.
- PySpark enables **scalable data transformations** using lazy evaluation.
- Databricks notebooks offer an **interactive and efficient development environment**.

---

### 🛠️ Tools & Technologies:
- Databricks Community Edition
- PySpark

---

### 📚 Learning References & Acknowledgements:
This learning initiative is supported by the data community and learning resources from:
- **Databricks** – https://www.databricks.com
- **Codebasics** – https://www.codebasics.io
- **Indian Data Club** – https://indiandataclub.com


### 🔖 Tags & Mentions:
#Databricks #Codebasics #IndianDataClub #DatabricksWithIDC









