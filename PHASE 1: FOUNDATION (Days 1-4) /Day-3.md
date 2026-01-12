# **Day 3: PySpark Transformations Deep Dive**

---

## 📘 Learnings:

🔹 𝗣𝘆𝗦𝗽𝗮𝗿𝗸 𝘃𝘀 𝗣𝗮𝗻𝗱𝗮𝘀
- Pandas is suitable for small, in-memory datasets, offering fast and flexible data manipulation.
- PySpark supports distributed processing, making it ideal for large-scale data with better performance and fault tolerance.

🔹 𝗝𝗼𝗶𝗻𝘀 (𝗜𝗻𝗻𝗲𝗿, 𝗟𝗲𝗳𝘁, 𝗥𝗶𝗴𝗵𝘁, 𝗢𝘂𝘁𝗲𝗿)
- Joins combine multiple datasets using a common key, enabling relationships across different tables.
- In PySpark, joins are optimized for large data volumes and are essential for building analytical datasets from raw tables.

🔹 𝗪𝗶𝗻𝗱𝗼𝘄 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝘀 (𝗥𝘂𝗻𝗻𝗶𝗻𝗴 𝗧𝗼𝘁𝗮𝗹𝘀, 𝗥𝗮𝗻𝗸𝗶𝗻𝗴𝘀)
- Window functions enable calculations like running totals, cumulative counts, and rankings while preserving the original row-level data.
- They are especially useful for user behavior and time-based analysis, where comparisons across rows are required without aggregation.

🔹 𝗨𝘀𝗲𝗿-𝗗𝗲𝗳𝗶𝗻𝗲𝗱 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝘀 (𝗨𝗗𝗙𝘀)
- UDFs enable custom business logic when built-in Spark functions are insufficient, making them useful for complex transformations and feature engineering.
- They should be used cautiously, as UDFs can impact performance compared to native Spark functions and may reduce optimization benefits.

---

## 🛠️ Hands-on Tasks Completed (Databricks Notebook):

- Loaded the full e-commerce dataset
- Performed complex joins across datasets
- Calculated running totals using window functions
- Created derived features for deeper insights

--- 

## Practice Exercise:

```sql

# Import in PySpark

from pyspark.sql import functions as F
from pyspark.sql.window import Window


1. Load Data into the dataframe
--------------------------------
df = spark.read.csv("/Volumes/Workspace/ecommerce/ecommerce_data/2019-Oct.csv", header=True, inferSchema=True)


2. Creating dataframes of the datsets, before performing Joins
---------------------------------------------------------------
## Creating dataframe "products_df"
products_df = df.select("product_id", "category_id", "category_code", "brand", "price").distinct()
display(products_df)

## Creating dataframe "events_df"
events_df = df.select("event_time", "event_type", "product_id", "user_id").distinct()
display(events_df)


3. Top 5 products by revenue
-----------------------------
from pyspark.sql import functions as F

revenue_df = (df.filter(F.col("event_type") == "purchase")
            .groupBy("product_id", "brand")
            .agg(F.sum("price").alias("revenue"))
            .orderBy(F.desc("revenue"))
            .limit(5)
)
print("Top 5 Products by Revenue:")
display(revenue_df)

# Note: Using 'brand' as 'product_name' is missing from the Kaggle dataset schema


4. Window definition
---------------------
window = Window.partitionBy("user_id").orderBy("event_time")



5. Running total (cumulative events per user)
----------------------------------------------

from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Running total (cumulative events per user)
df_with_running_total = df.withColumn(
    "cumulative_events",
    F.count("*").over(window)
)
display(df_with_running_total.limit(10))



6. Conversion rate by category
-------------------------------

from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Conversion rate by category
conversion_df = (
    df.groupBy("category_code")
      .pivot("event_type")
      .count()
      .withColumn(
          "conversion_rate",
          F.round(F.col("purchase") / F.col("view") * 100, 2)
      )
)
display(conversion_df)


```

---

## 📚 Learning References & Acknowledgements:
This learning initiative is supported by the data community and learning resources from:

- Databricks – https://www.databricks.com
- Codebasics – https://www.codebasics.io
- Indian Data Club – https://indiandataclub.com


## 🔖 Tags & Mentions:
@Databricks @Codebasics @IndianDataClub #DatabricksWithIDC
