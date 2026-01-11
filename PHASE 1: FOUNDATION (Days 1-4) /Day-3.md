# **Day 3: PySpark Transformations Deep Dive**

---

## 🔍 Topics Learned:

𝗣𝘆𝗦𝗽𝗮𝗿𝗸 𝘃𝘀 𝗣𝗮𝗻𝗱𝗮𝘀
- Pandas works well for small, in-memory datasets, but 𝗣𝘆𝗦𝗽𝗮𝗿𝗸 𝗲𝗻𝗮𝗯𝗹𝗲𝘀 𝗱𝗶𝘀𝘁𝗿𝗶𝗯𝘂𝘁𝗲𝗱 𝗽𝗿𝗼𝗰𝗲𝘀𝘀𝗶𝗻𝗴, making it suitable for large-scale data with better performance and fault tolerance.

𝗝𝗼𝗶𝗻𝘀 (𝗜𝗻𝗻𝗲𝗿, 𝗟𝗲𝗳𝘁, 𝗥𝗶𝗴𝗵𝘁, 𝗢𝘂𝘁𝗲𝗿)
- Joins allow combining multiple datasets based on a common key. In PySpark, joins are optimized for l𝗮𝗿𝗴𝗲 𝗱𝗮𝘁𝗮 𝘃𝗼𝗹𝘂𝗺𝗲𝘀 and are essential for building analytical datasets from raw tables.

𝗪𝗶𝗻𝗱𝗼𝘄 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝘀 (𝗥𝘂𝗻𝗻𝗶𝗻𝗴 𝗧𝗼𝘁𝗮𝗹𝘀, 𝗥𝗮𝗻𝗸𝗶𝗻𝗴𝘀)
- Window functions help calculate metrics like cumulative counts, running totals, and rankings without reducing the number of rows — extremely useful for 𝘂𝘀𝗲𝗿 𝗯𝗲𝗵𝗮𝘃𝗶𝗼𝗿 𝗮𝗻𝗱 𝘁𝗶𝗺𝗲-𝗯𝗮𝘀𝗲𝗱 𝗮𝗻𝗮𝗹𝘆𝘀𝗶𝘀.

𝗨𝘀𝗲𝗿-𝗗𝗲𝗳𝗶𝗻𝗲𝗱 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻𝘀 (𝗨𝗗𝗙𝘀)
- UDFs allow applying custom business logic when built-in Spark functions are not sufficient, helping in feature engineering, though they should be used carefully due to performance impact.

---

### 🛠️ Hands-on Tasks Completed (Databricks Notebook):

- Loaded the full e-commerce dataset
- Performed complex joins across datasets
- Calculated running totals using window functions
- Created derived features for deeper insights

--- 

###  📚 Learning References & Acknowledgements:
This learning initiative is supported by the data community and learning resources from:
