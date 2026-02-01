# ELT Pipeline Orchestration leveraging Kestra, and GCP

## Objective
The goal of this project is to build an **Extract, Load, and Transform (ELT) pipeline**  using **NYC Taxi Data** set, leveraging **Kestra**, **Google Cloud Storage (GCS)**, and **BigQuery**. This pipeline can be scheduled to run at the beginning of each month, while any previously missing month can be captured using **backfilling**.
## Dataset
The dataset used in this project can be found [here](https://github.com/DataTalksClub/nyc-tlc-data/releases/tag/green/download)

## Functionality
***Extract***: The data is first extracted from the link shown in the **Dataset** section.

***Load***: The extracted data is then loaded onto the **GCS bucket** which acts as a  **Data Lake** .

***Transform***: The loaded data then is queried from **BigQuery** to compute a **Unique Record ID** and **filename**.  The result is then saved into a **BigQuery** table which is **partitioned by date** to achieve query efficiency.





