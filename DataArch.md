## 🛠️ Data Architecture & Pipeline

* **Data Sources:** One large CSV file
* **ETL Processes (Power Query / M):**
  * As the data was flat and we needed to break it apart in order to create our star schema. I referenced the original source and disabled load in order to create the other tables.
  * I create my dimension tables; product, customer and geography. Then created my fact table called sales.\
  * Removed columns that were not needed.
  * Removed duplicates from the dimension tables.
  * Merged certain columns to create composite keys to then create relationships. (Due to limitations in the data source, some of those keys have a data type of text, which is not ideal. In the real work, I would create an integer surrogate key upstream or perhaps even in Power Query) 
  * Removed duplicate transaction.
  * Upon checking, there were no NULL values.
