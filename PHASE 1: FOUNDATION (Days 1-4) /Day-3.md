# **Day 3: PySpark Transformations Deep Dive**

---

## 📘 Learnings:

🔹 𝗣𝘆𝗦𝗽𝗮𝗿𝗸 𝘃𝘀 𝗣𝗮𝗻𝗱𝗮𝘀
- Pandas works well for small, in-memory datasets, but 𝗣𝘆𝗦𝗽𝗮𝗿𝗸 𝗲𝗻𝗮𝗯𝗹𝗲𝘀 𝗱𝗶𝘀𝘁𝗿𝗶𝗯𝘂𝘁𝗲𝗱 𝗽𝗿𝗼𝗰𝗲𝘀𝘀𝗶𝗻𝗴, making it suitable for large-scale data with better performance and fault tolerance.

𝗝𝗼𝗶𝗻𝘀 (𝗜𝗻𝗻𝗲𝗿, 𝗟𝗲𝗳𝘁, 𝗥𝗶𝗴𝗵𝘁, 𝗢𝘂𝘁𝗲𝗿)
- Joins allow combining multiple datasets based on a common key. In PySpark, joins are optimized for l𝗮𝗿𝗴𝗲 𝗱𝗮𝘁𝗮 𝘃𝗼𝗹𝘂𝗺𝗲𝘀 and are essential for building analytical datasets from raw tables.

𝗪𝗶𝗻𝗱𝗼𝘄 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝘀 (𝗥𝘂𝗻𝗻𝗶𝗻𝗴 𝗧𝗼𝘁𝗮𝗹𝘀, 𝗥𝗮𝗻𝗸𝗶𝗻𝗴𝘀)
- Window functions help calculate metrics like cumulative counts, running totals, and rankings without reducing the number of rows — extremely useful for 𝘂𝘀𝗲𝗿 𝗯𝗲𝗵𝗮𝘃𝗶𝗼𝗿 𝗮𝗻𝗱 𝘁𝗶𝗺𝗲-𝗯𝗮𝘀𝗲𝗱 𝗮𝗻𝗮𝗹𝘆𝘀𝗶𝘀.

𝗨𝘀𝗲𝗿-𝗗𝗲𝗳𝗶𝗻𝗲𝗱 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝘀 (𝗨𝗗𝗙𝘀)
- UDFs allow applying custom business logic when built-in Spark functions are not sufficient, helping in feature engineering, though they should be used carefully due to performance impact.

---

## 🛠️ Hands-on Tasks Completed (Databricks Notebook):

- Loaded the full e-commerce dataset
- Performed complex joins across datasets
- Calculated running totals using window functions
- Created derived features for deeper insights

--- 

## Practice Exercise:

```sql
from pyspark.sql import functions as F
from pyspark.sql.window import Window

1 Load Data into the dataframe.
df = spark.read.csv("/Volumes/Workspace/ecommerce/ecommerce_data/2019-Oct.csv", header=True, inferSchema=True)



2 Top 5 products by revenue
revenue = (events.filter(F.col("event_type") == "purchase") \
    .groupBy("product_id", "product_name") \
    .agg(F.sum("price").alias("revenue")) \
    .orderBy(F.desc("revenue")).limit(5)
)
display(revenue)

| product_id | category_code          | revenue       |
| ---------- | ---------------------- | ------------- |
| 1005115    | electronics.smartphone | 12,406,807.35 |
| 1005105    | electronics.smartphone | 10,239,248.68 |
| 1004249    | electronics.smartphone | 6,730,112.92  |
| 1005135    | electronics.smartphone | 5,567,806.64  |
| 1004767    | electronics.smartphone | 5,430,723.43  |



3 Running total per user
from pyspark.sql import functions as F
from pyspark.sql.window import Window



4 Window definition
window = Window.partitionBy("user_id").orderBy("event_time")



5 Running total (cumulative events per user)
df_with_running_total = df.withColumn(
    "cumulative_events",
    F.count("*").over(window)
)

display(df_with_running_total.limit(10))

| event_time           | event_type | product_id | category_id | category_code                       | brand    | price  | user_id   | user_session | cumulative_events |
| -------------------- | ---------- | ---------- | ----------- | ----------------------------------- | -------- | ------ | --------- | ------------ | ----------------- |
| 2019-10-09T10:30:19Z | view       | 17301541   | 2.05301E+18 | null                                | null     | 162.17 | 205053188 | e1eadbc6…    | 1                 |
| 2019-10-09T10:30:44Z | view       | 17301541   | 2.05301E+18 | null                                | null     | 162.17 | 205053188 | e1eadbc6…    | 2                 |
| 2019-10-07T06:23:01Z | view       | 16200119   | 2.05301E+18 | kids.fmcg.diapers                   | moony    | 18.47  | 222907508 | cb653adc…    | 1                 |
| 2019-10-07T06:26:23Z | view       | 16200162   | 2.05301E+18 | kids.fmcg.diapers                   | moony    | 18.47  | 222907508 | cb653adc…    | 2                 |
| 2019-10-08T14:29:09Z | view       | 6200883    | 2.05301E+18 | appliances.environment.air_heater   | elenberg | 46.31  | 244673419 | e2f0524c…    | 1                 |
| 2019-10-12T10:15:48Z | view       | 17300355   | 2.05301E+18 | null                                | creed    | 240.16 | 257849716 | 71e76013…    | 1                 |
| 2019-10-22T22:05:40Z | view       | 3900896    | 2.05301E+18 | appliances.environment.water_heater | klima    | 77.20  | 266203246 | c83d6f3d…    | 1                 |
| 2019-10-24T01:14:36Z | view       | 3900896    | 2.05301E+18 | appliances.environment.water_heater | klima    | 77.20  | 266203246 | 56944410…    | 2                 |
| 2019-10-06T11:29:22Z | view       | 22700574   | 2.05301E+18 | null                                | null     | 88.81  | 278272605 | e4cd7037…    | 1                 |
| 2019-10-06T11:30:58Z | view       | 22700129   | 2.05301E+18 | null                                | stels    | 66.93  | 278272605 | 0a20874c…    | 2                 |




6 Conversion rate by category
from pyspark.sql import functions as F

conversion_df = (
    events
    .filter(F.col("category_code").isNotNull())
    .groupBy("category_code", "event_type")
    .count()
    .groupBy("category_code")
    .pivot("event_type", ["view", "purchase"])
    .sum("count")
    .fillna(0)
    .withColumn(
        "conversion_rate",
        F.when(F.col("view") > 0,
               (F.col("purchase") / F.col("view")) * 100
        ).otherwise(0)
    )
)

display(conversion_df)


| category_code                       | view     | purchase | conversion_rate |
| ----------------------------------- | -------- | -------- | --------------- |
| auto.accessories.parktronic         | 12305    | 46       | 0.3738          |
| furniture.living_room.sofa          | 215471   | 1084     | 0.5031          |
| stationery.cartrige                 | 7380     | 134      | 1.8157          |
| sport.bicycle                       | 128759   | 838      | 0.6508          |
| apparel.sock                        | 2621     | 21       | 0.8012          |
| appliances.environment.fan          | 2172     | 27       | 1.2431          |
| kids.swing                          | 31596    | 330      | 1.0444          |
| electronics.audio.microphone        | 28394    | 430      | 1.5144          |
| auto.accessories.radar              | 42350    | 494      | 1.1665          |
| electronics.clocks                  | 1272783  | 17906    | 1.4068          |
| electronics.audio.music_tools.piano | 35409    | 423      | 1.1946          |
| appliances.kitchen.hood             | 105149   | 936      | 0.8902          |
| appliances.kitchen.meat_grinder     | 155551   | 2382     | 1.5313          |
| electronics.tablet                  | 301992   | 5603     | 1.8553          |
| apparel.underwear                   | 44374    | 97       | 0.2186          |
| appliances.kitchen.coffee_machine   | 81826    | 544      | 0.6648          |
| furniture.bathroom.toilet           | 16495    | 182      | 1.1034          |
| furniture.bedroom.blanket           | 22470    | 162      | 0.7210          |
| furniture.living_room.chair         | 71421    | 648      | 0.9073          |
| appliances.environment.air_heater   | 153390   | 2483     | 1.6187          |
| appliances.iron                     | 157645   | 3653     | 2.3172          |
| electronics.audio.headphone         | 1018542  | 30503    | 2.9948          |
| kids.fmcg.diapers                   | 24203    | 768      | 3.1732          |
| computers.notebook                  | 1106406  | 15590    | 1.4091          |
| electronics.smartphone              | 10619448 | 338018   | 3.1830          |
| appliances.kitchen.refrigerators    | 863411   | 11218    | 1.2993          |
| electronics.video.tv                | 1055961  | 21565    | 2.0422          |
| appliances.environment.water_heater | 138784   | 2774     | 1.9988          |


```

---

## 📚 Learning References & Acknowledgements:
This learning initiative is supported by the data community and learning resources from:

- Databricks – https://www.databricks.com
- Codebasics – https://www.codebasics.io
- Indian Data Club – https://indiandataclub.com


## 🔖 Tags & Mentions:
@Databricks @Codebasics @IndianDataClub #DatabricksWithIDC
