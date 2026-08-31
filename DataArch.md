## 🛠️ Data Architecture & Pipeline

* **Data Source:** Single flat CSV file containing raw transactional data.
* **ETL & Data Transformation (Power Query / M):**
  * **Star Schema Preparation:** Referenced the original source table and disabled its load to break the flat dataset apart into dedicated Fact and Dimension tables.
  * **Dimension & Fact Creation:** Separated data into `Dim_Customer`, `Dim_Product`, and `Dim_Geography` dimension tables, alongside the central `Fact_Sales` table.
  * **Data Cleansing:** Removed redundant columns, eliminated duplicate records across dimension tables, and verified zero `NULL` values.
  * **Composite Keys:** Merged columns to create composite keys for table relationships. 
    > *Note:* Due to source data limitations, some keys use a `Text` data type. In a production environment, I would generate integer surrogate keys upstream or within Power Query to optimize storage and query performance.
