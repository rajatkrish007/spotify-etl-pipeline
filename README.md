# Spotify ETL Pipeline

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

---

### 📸 **Architecture Diagram**
*(Add architecture image here)*

### 📊 **Sample Data Visualization**
*(Add charts or analysis results here)*

