# **DAY 1 – Platform Setup & First Steps**

## Learn:
- Why Databricks vs Pandas/Hadoop?
- Lakehouse architecture basics
- Databricks workspace structure
- Industry use cases (Netflix, Shell, Comcast)

## 🛠️ Tasks:
1. Create Databricks Community Edition account
2. Navigate Workspace, Compute, Data Explorer
3. Create first notebook
4. Run basic PySpark commands

## Practice:

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

|-------|-----|
|product|price|
|-------|-----|
|MacBook| 1299|
|-------|-----|

