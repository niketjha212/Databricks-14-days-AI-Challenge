📅 Day 1 – Platform Setup and First Steps

🔹 What I Learned:
- Why Databricks vs Pandas/Hadoop ?
- Lakehouse architecture difference
- Databricks workspace structure
- Industry use cases (Netflix, Shell, Comcast)

🔹 Tasks:
1. Create Databricks Community Edition account
2. Navigate Workspace, Compute, Data Explorer
3. Create first notebook
4. Run basic PySpark commands

🔹 Practice:

# Create simple DataFrame
data = [("iPhone", 999), ("Samsung", 799), ("MacBook", 1299)]
df = spark.createDataFrame(data, ["product", "price"])
df.show()

# Filter expensive products
df.filter(df.price > 1000).show()
