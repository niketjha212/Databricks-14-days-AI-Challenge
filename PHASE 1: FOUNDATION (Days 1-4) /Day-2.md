# 𝗗𝗮𝘆-𝟮: Apache Spark Fundamentals

---

## Things Learnt:
- Spark Architecture: Understood the roles of Driver, Executors, and how Spark uses DAG (Directed Acyclic Graph) to optimize execution.
- DataFrames vs RDDs : Learned why DataFrames are preferred over RDDs due to optimization, ease of use, and Catalyst optimizer.
- Lazy Evaluation : Spark doesn’t execute immediately — actions trigger execution, helping Spark optimize the entire workflow efficiently.
- Notebook Magic Commands :Got hands-on with Databricks magic commands like: %sql, %python, %fs for seamless multi-language execution.
- Importance of col() – Used to refer to columns in PySpark for transformations, filtering, null checks, and calculations

--- 

## Tasks Completed:
- Uploaded a sample e-commerce CSV file.
- Created a DataFrame using PySpark
- Performed basic operations : select(), show(), dtypes(), filter(), groupBy(), orderBy()
- Used col() to handle columns safely and perform null checks.

## Exercise:

#Load Data into the dataframe.
df = spark.read.csv("/Volumes/Workspace/ecommerce/ecommerce_data/2019-Oct.csv", header=True, inferSchema=True)
display(df)

| event_time                    | event_type | product_id | category_id         | category_code                       | brand    | price   | user_id   | user_session                         |
| ----------------------------- | ---------- | ---------- | ------------------- | ----------------------------------- | -------- | ------- | --------- | ------------------------------------ |
| 2019-10-01T00:00:00.000+00:00 | view       | 44600062   | 2103807459595387724 | null                                | shiseido | 35.79   | 541312140 | 72d76fde-8bb3-4e00-8c23-a032dfed738c |
| 2019-10-01T00:00:00.000+00:00 | view       | 3900821    | 2053013552326770905 | appliances.environment.water_heater | aqua     | 33.20   | 554748717 | 9333dfbd-b87a-4708-9857-6336556b0fcc |
| 2019-10-01T00:00:01.000+00:00 | view       | 17200506   | 2053013559792632471 | furniture.living_room.sofa          | null     | 543.10  | 519107250 | 566511c2-e2e3-422b-b695-cf8e6e792ca8 |
| 2019-10-01T00:00:01.000+00:00 | view       | 1307067    | 2053013558920217191 | computers.notebook                  | lenovo   | 251.74  | 550050854 | 7c90fc70-0e80-4590-96f3-13c02c18c713 |
| 2019-10-01T00:00:04.000+00:00 | view       | 1004237    | 2053013555631882655 | electronics.smartphone              | apple    | 1081.98 | 535871217 | c6bd7419-2748-4c56-95b4-8cec9ff8b80d |
| 2019-10-01T00:00:05.000+00:00 | view       | 1480613    | 2053013561092866779 | computers.desktop                   | pulser   | 908.62  | 512742880 | 0d0d91c2-c9c2-4e81-90a5-86594dec0db9 |
| 2019-10-01T00:00:08.000+00:00 | view       | 17300353   | 2053013553853497655 | null                                | creed    | 380.96  | 555447699 | 4fe811e9-91de-46da-90c3-bbd87ed3a65d |
| 2019-10-01T00:00:08.000+00:00 | view       | 31500053   | 2053013558031024687 | null                                | luminarc | 41.16   | 550978835 | 6280d577-25c8-4147-99a7-abc6048498d6 |
| 2019-10-01T00:00:10.000+00:00 | view       | 28719074   | 2053013565480109009 | apparel.shoes.keds                  | baden    | 102.71  | 520571932 | ac1cd4e5-a3ce-4224-a2d7-ff660a105880 |
| 2019-10-01T00:00:11.000+00:00 | view       | 1004545    | 2053013555631882655 | electronics.smartphone              | huawei   | 566.01  | 537918940 | 406c46ed-90a4-4787-a43b-59a410c1a5fb |




# Basic operations to see columns - product_id, brand and price.
df.select("product_id", "brand",  "price").show(10)


|product_id|   brand|  price|
|----------|--------|-------|
|  44600062|shiseido|  35.79|
|   3900821|    aqua|   33.2|
|  17200506|    NULL|  543.1|
|   1307067|  lenovo| 251.74|
|   1004237|   apple|1081.98|
|   1480613|  pulser| 908.62|
|  17300353|   creed| 380.96|
|  31500053|luminarc|  41.16|
|  28719074|   baden| 102.71|
|   1004545|  huawei| 566.01|


# filter by price greater than 100.
df.filter("price > 100").count()

| 27750807 |


# Count of types of events.
df.groupBy("event_type").count().show()

|event_type|   count|
|----------|--------|
|  purchase|  742849|
|      cart|  926516|
|      view|40779399|

# Count of top brands.
top_brands = df.groupBy("brand").count().orderBy("count", ascending=False).limit(5)
top_brands.show()

|  brand|  count|
|--------|------|
|   NULL|6113008|
|samsung|5282775|
|  apple|4122554|
| xiaomi|3083763|
| huawei|1111205|


--- 

## 📚 Learning References & Acknowledgements:
This learning initiative is supported by the data community and learning resources from:

- Databricks – https://www.databricks.com
- Codebasics – https://www.codebasics.io
- Indian Data Club – https://indiandataclub.com


## 🔖 Tags & Mentions:
@Databricks @Codebasics @IndianDataClub #DatabricksWithIDC
