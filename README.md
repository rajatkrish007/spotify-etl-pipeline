# Spotify ETL Pipeline
#

## Overview
The **Spotify ETL Pipeline** is designed to extract, transform, and load Spotify data using **Python, AWS services, and automation triggers**. This pipeline pulls data from the **Spotify API** using Spotipy, processes it through AWS Lambda functions, and stores it in **Amazon S3, AWS Glue, and Athena** for analysis. 


## Architecture
The pipeline follows an **ETL (Extract, Transform, Load)** architecture, leveraging AWS services:

- **Extract**: Fetch data from Spotify API using AWS Lambda.
- **Transform**: Process and clean the data using another AWS Lambda function.
- **Load**: Store transformed data in S3 and query it using AWS Glue and Athena.
- **Automation**: Event-driven triggers using Amazon CloudWatch and S3 events.
  

![ETL architecture ](https://github.com/user-attachments/assets/11339c56-40fe-465e-a887-4f51d5a08872)



## Technologies Used
- **Python** (Spotipy library for API interaction, Pandas for data transformation)
- **AWS Lambda** (serverless functions for extraction and transformation)
- **Amazon S3** (storage for raw and processed data)
- **AWS Glue** (schema inference and data cataloging)
- **Amazon Athena** (querying and analysis)
- **AWS EventBridge (CloudWatch)** (triggers for automation)

## Workflow

### 1. Create a Spotify Developer App
- Register on [Spotify for Developers](https://developer.spotify.com/).
- Create an **App** to generate `Client ID` and `Client Secret`.
- Set up **Redirect URI** and obtain authorization tokens.

### 2. Authentication & Authorization
- Use **Spotipy** Python library to authenticate using `Client ID` and `Client Secret`.
- Generate an access token to interact with the Spotify API.

### 3. AWS Lambda Functions
#### **Lambda 1: Data Extraction**
- Pulls data from the **Spotify API** (e.g., playlists, tracks, artists, albums).
- Extracts useful data from JSON format using **Pandas**:
  - Album data, Artist data, and Songs data are extracted into lists.
  - These lists are then converted into **Pandas DataFrames** for further operations.
- Stores raw data in **Amazon S3** (Raw Data Bucket).
- Triggered daily using **Amazon EventBridge (CloudWatch Rule)**.

#### **Lambda 2: Data Transformation**
- Reads raw data from **Amazon S3**.
- Cleans, structures, and transforms the data using **Pandas**.
- Stores transformed data in another **Amazon S3 bucket**.
- Triggered by an **S3 event** when new raw data is uploaded.

### 4. AWS Glue & Athena
- **AWS Glue Crawler** infers schema from the transformed S3 data.
- Creates a **Glue Data Catalog** to structure the data.
- **Amazon Athena** enables SQL-based querying on the cataloged data.

## Operations Performed in the Project
1. **Extracting JSON data from Spotify API**
2. **Parsing JSON and extracting relevant fields**
   - Album Data (Album Name, Release Date, Total Tracks)
   - Artist Data (Artist Name, Genre, Popularity)
   - Songs Data (Track Name, Duration, Explicit, Album ID, Artist ID)
3. **Converting extracted lists to Pandas DataFrames**
4. **Cleaning and structuring the DataFrames**
5. **Uploading raw and transformed data to S3**
6. **Schema inference using AWS Glue**
7. **Querying processed data using Athena**

## Automation
- **CloudWatch EventBridge** triggers the Extraction Lambda daily.
- **S3 Event Triggers** initiate the Transformation Lambda when new data is added.
- **Glue Crawler** runs periodically to update the schema.

## Setup & Deployment
### Prerequisites
- AWS account with permissions for **Lambda, S3, Glue, Athena, EventBridge**.
- Spotify Developer account with **Client ID & Secret**.
- Python installed locally for testing.

### Steps
1. Deploy the **Extraction Lambda** with Spotify API authentication.
2. Configure **EventBridge CloudWatch Rule** for scheduled execution.
3. Deploy the **Transformation Lambda** to process raw data.
4. Set up **S3 Event Trigger** to run Transformation Lambda.
5. Configure **Glue Crawler** to infer schema from transformed data.
6. Use **Amazon Athena** to analyze data using SQL queries.

## Example Query in Athena
```sql
SELECT artist_name, COUNT(track_id) AS track_count
FROM spotify_data
GROUP BY artist_name
ORDER BY track_count DESC
LIMIT 10;
```

## Future Enhancements
- Implement **Redshift or DynamoDB** for faster querying.
- Add **additional data points** from the Spotify API (e.g., audio features).
- Create a **dashboard in Power BI or Tableau** for visualization.

## Conclusion
This **Spotify ETL Pipeline** automates the extraction, transformation, and loading of Spotify data using AWS, enabling efficient data analysis through Athena. 🚀

## Project Snapshots

### AWS S3 
![s3 ss](https://github.com/user-attachments/assets/f38b47e7-3218-4f19-8510-7498c88dc236)
#

### AWS Lambda 
![lamda ss1](https://github.com/user-attachments/assets/ae5dfb1e-db4a-4cbf-b36a-3307169ec666)
#

![lamda ss2](https://github.com/user-attachments/assets/031bd027-26ee-4eb0-aee8-a3a4092c6cbb)
#

![lambda ss3](https://github.com/user-attachments/assets/2c4ec46e-8797-4be8-a335-9c4611d15062)
#

![lambda ss4](https://github.com/user-attachments/assets/a8331584-ab4f-49db-a239-c5301eb115ad)
#

![lambda ss5 1](https://github.com/user-attachments/assets/1632de98-c1e0-48a4-9dfe-b93e13dc315f)
#

![lambda ss5 2](https://github.com/user-attachments/assets/74b7157c-cac3-4871-b8be-8830558fe5ea)
#

![lambda ss5 3](https://github.com/user-attachments/assets/490e27e3-ca7b-4108-89ce-a3da1dc6bbbd)
#

### AWS Glue 
![crawlers ss](https://github.com/user-attachments/assets/3ab4cce5-8087-481e-92c7-83a1808a4020)

![tables ss](https://github.com/user-attachments/assets/306633bc-c5bb-4b06-af00-81f885fca1b9)
#

### AWS Athena - Querying Album, Artist, and Songs Data

(Performing SQL-based analysis on structured Spotify data stored in AWS Athena)


![code](https://github.com/user-attachments/assets/d5604176-1758-461f-9d2c-57cfc1d3104a)
#

![output](https://github.com/user-attachments/assets/a911cc77-7474-4664-bafd-c26222a21521)
#

![analysis_on_album_data_code](https://github.com/user-attachments/assets/58e43566-ed77-4fc8-9286-24563c708593)
#

![analysis_on_album_data_output](https://github.com/user-attachments/assets/26636e9d-1f54-46d6-b10f-007b8024b8f0)
#

![code](https://github.com/user-attachments/assets/70bcf2b7-591b-4652-a2dd-530d662e2d3f)
#

![output](https://github.com/user-attachments/assets/86fe2a11-ad87-4064-9cde-1a3863f9e291)
#

![code(athena)](https://github.com/user-attachments/assets/447ca38c-3196-4abb-8d0e-be2cd84962a5)
#

![output(athena)](https://github.com/user-attachments/assets/b52ccbf5-bc9f-4ed4-92e7-c2ae543e8517)
#

![analysis_on_songs_data_code](https://github.com/user-attachments/assets/756b0ac6-02a0-4479-bbae-ceed804b8fbe)
#

![analysis_on_songs_data_output](https://github.com/user-attachments/assets/8daec2f6-768c-4dfc-834b-43e6690e5374)














