# ELT Pipeline Orchestration leveraging Kestra, and GCP

## Objective
The goal of this project is to build an **Extract, Load, and Transform (ELT) pipeline**  using **NYC Taxi Data** set, leveraging **Kestra**, **Google Cloud Storage (GCS)**, and **BigQuery**. This pipeline can be scheduled to run at the beginning of each month, while any previously missing month can be captured using **backfilling**.
## Dataset
The dataset used in this project can be found [here](https://github.com/DataTalksClub/nyc-tlc-data/releases/tag/green/download)

## Functionality
***Extract***: The data is first extracted from the link shown in the **Dataset** section.

***Load***: The extracted data is then loaded onto the **GCS bucket** which acts as a  **Data Lake** .

***Transform***: The loaded data then is queried from **BigQuery** to compute a **Unique Record ID** and **filename**.  The result is then saved into a **BigQuery** table which is **partitioned by date** to achieve query efficiency.

## Design Diagram 
![](system_diagram.png)

## How to run
### Setup
***Gemini API KEY (OPTIONAL)***: This is to enable co-pilot feature embedded within Kestra's API for code suggestion, and generation. 
```bash
cd pipeline/
export GEMINI_API_KEY="your-api-key-here"
```
***Adding GCP Service Account credential .json file into environment***: Execute the following after you download the .json file service account key file. Here our file name is "service-account.json". 
```bash
echo SECRET_GCP_SERVICE_ACCOUNT=$(cat service-account.json | base64 -w 0) >> .env_encoded
```
***Starting Kestra***: Run the docker compose up command. This will start Kestra UI at  **port 8080**. As per the docker compose file, the **username** is **admin@kestra.io**, and **password**  is **Admin1234!**


***GCP resources***: This is to store desired GCP location, GCS bucket, and BigQuery Dataset names into Kestra's KV store as environment variables. To do this, copy-paste the content of  **GCP_kv.yaml** file onto Kestra as a flow, and execute it.

***Initializing GCP resources***: To do this, copy-paste the content of  **GCP_setup.yaml** file onto Kestra as a flow, and execute it.

***Running the NYC Taxi Data ELT flow*** : To do this, copy-paste the content of  **GCP_taxi_scheduled.yaml** file onto Kestra as a flow, and execute it.